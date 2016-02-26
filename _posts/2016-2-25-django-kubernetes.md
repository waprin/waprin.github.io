---
layout: post
title: Deploying Django/Postgres/Redis on Kubernetes
description: ""
categories: tech
tags: [python, django, kubernetes]
---

<img height="300" width="600" src=
"{{ site.url }}/assets/djangokube.png" />

This article was cross posted to Medium.com.

Django is one of the most popular open-source web frameworks, and perhaps no Django user is more notable than Instagram, who went into deep detail on how they setup their Django stack on [their blog post](http://instagram-engineering.tumblr.com/post/13649370142/what-powers-instagram-hundreds-of-instances). While they use a variety of technologies, the most prominent parts of the stack are Django, PostgreSQL, and Redis. This series of blog posts will go into detail on how to deploy the entire stack on [Kubernetes](http://kubernetes.io), although the first part will focus on just Django using a database not running in Kubernetes.

This blog post is based on a presentation I gave to the Django San Francisco Meetup. You can check out this [slide deck](https://speakerdeck.com/waprin/deploying-django-on-kubernetes)..

# Prerequisites 

This will be a multi-part tutorial, and assumes you already have some familiarity with Django and connecting it to databases and caches. If you have’t used Django before, I first recommend working through it’s excellent tutorial.

It’s also helpful to have some understanding of containers, particularly [Docker](https://www.docker.com/), which you will need to install first. Refer to Docker documentation if you get confused. Docker only runs on Linux, but you can use it on Mac or Windows by running a Linux virtual machine. You interact with the Linux machine using Docker Machine, part of the standard Docker toolkit.

All the code for this tutorial can be found here:

[https://github.com/waprin/kubernetes_django_postgres_redis](https://github.com/waprin/kubernetes_django_postgres_redis)

This repo is my current best attempt at a full-stack Django/Postgres/Redis on Container Engine, but for this first blog post, we are going to focus on setting up Container Engine (Kubernetes on Google Cloud) and deploying just Django to it. We’ll skip Redis and Postgres for now, and just use SQLite the in-memory cache. If you want to skip ahead of the class, read the entire README.md from the repo for plain instructions on deploying the whole project.

If you have any issues, use the Github Issue Tracker. If you have any improvements, submit a Pull Request. You can also bug me on Twitter.

# Introducing Kubernetes 

Traditionally, you would probably deploy Django to some sort of virtual machine instance. The downside is that if you want to install other applications on the same machine, there might be library conflicts. It was also hard to reproduce your application state without taking a machine image, which tend to be non-portable and slow to start.

Containers, most often using the Docker format are a great way to produce application images that are immutable, quick to spin up, and isolated from other applications. But when you want to deploy a group of containers to a cluster, you face a bunch of challenges.

* How does a container get scheduled on a machine?
* How does a container talk to another container, even it’s on different machine?
* Where do I store my data and my secrets?
* How do I scale it, manually and automatically?
* How do I make sure my container stay healthy and are replaced on failure?
* How do I safely deploy new containers and roll back bad ones?
* How do I handle namespaces and authorization?

Kubernetes is an entirely open-source project started by Google to help address these issues. It provides a container scheduler and a large collection of features to provide the tools to build your container-based platform on top of a cluster of machines, virtual or bare-metal.

Google Cloud offers a product called Container Engine which provides a fully-managed Kubernetes, so you never have to administer your own Kubernetes cluster. If you’re the type who prefers to handle all your own operations though, you can always run Kubernetes yourself on Google Compute Engine, Amazon EC2, other cloud VPS providers, or on your own hardware. You can even run a single-node cluster locally using Vagrant.

Making sure Kubernetes runs smoothly on a variety of platforms is a large community effort. Fortunately, Kubernetes has a vibrant community, and is always looking for new contributors to help improve it.

## Core Kubernetes Concepts 

Before we get into deploying Django, it’s good to review a few core Kubernetes concepts.

* <strong>Nodes</strong> — Nodes are the Linux machines running the Docker containers that make up the cluster. Usually these will be cloud VPS instances, although for those running Kubernetes on-premise, they may be actual machines. 
* <strong>Pods</strong> — This is the basic unit of orchestration. A Pod has one or more container running inside it. A Pod can have an arbitrary amount of Labels, which are used by Services and Replication Controllers to match with Pods.
* <strong>Replication Controller</strong> — A Replication Controller controls how many of a given Pod exist, based on a provided label. You might want exactly 1, or 10 of a given Pod, and a Replication Controller will monitor your Pods and start up new ones in case of failure. You can manually or automatically scale these up or down.
* <strong>Service</strong> — A Service is how a Pod talks to another Pod, even if they’re on different Nodes. A Service provides an IP on a virtual private network (10.0.0.0/8) created by Kubernetes, and that IP will round-robin to different Pods that match a given Label. The IP for the service can be discovered using either environment variables, or the recommended Kube-DNS add-on. 

# Step 1: Run The App Locally 

The first step setup a Python development environment. Follow these instructions for setting it up on 
[OS X](http://docs.python-guide.org/en/latest/starting/install/osx/), 
[Linux](http://docs.python-guide.org/en/latest/starting/install/linux/) , or 
[Windows](http://docs.python-guide.org/en/latest/starting/install/win/).

I am also a big fan of 
[virtualenvwrappers](https://virtualenvwrapper.readthedocs.org/en/latest/) for some nice aliases to create a virtualenv.

{% highlight bash %}
$ mkvirtualenv guestbook
$ git clone https://github.com/waprin/kubernetes_django_postgres_redis
$ cd guestbook
$ pip install -r requirements.txt
{% endhighlight %}


The Django app has been configured to accept an environment variable that will specify whether or not we want to connect to a real database and cache, called NODB. In later posts, we’ll disable NODB and talk to Postgers and Redis, but for now, let’s keep it simple.

{% highlight bash %}

$ export NODB=1
{% endhighlight %}

Now we can take a look at the what the app looks like on our local workstation using the Django development server

{% highlight bash %}
$ python manage.py runserver
{% endhighlight %}


We can see the app and make a few guestbook posts by following the link in your web browser:

{% highlight bash %}
http://locahost:8000
{% endhighlight %}

You should see:

<img height="400" width="600" src="{{ site.url }}/assets/guestbook.png" />


If you see an error about missing tables or not being able to connect to a database, you probably did not properly export NODB=1 to your environment.

# Step 2: Creating the Container 

To deploy our app to Kubernetes, the first step is to make a Docker image to deploy.

We have a typical Django app, which consist of a root directory which container our project directory and a directory for each app in our project.

We need to have a server that will serve our Django app, and the local development server created by 'python manage.py runserver' is not recommended for production use. We could use any server that can talk to Django via WSGI, including Apache, but for this case we will go with Gunicorn which is a popular choice to serve Django apps.

Starting from a simple Linux distro like Ubuntu, we need to install several Python dependencies using apt-get and a few Python dependencies such as pip.

For the initial setup, my Dockerfile extends a base image that accomplishes that.

{% highlight bash %}

# https://github.com/GoogleCloudPlatform/python-docker
FROM gcr.io/google_appengine/python

Despite the name, this base Dockerfile is not specific to App Engine. You can follow the link to see exactly what’s installed.

We also need to install whatever dependencies our app needs, and the easiest way to do that is to actually create a virtualenv inside our container and run a `pip install` as part of the Docker build step.

# Create a virtualenv for the application dependencies.
# If you want to use Python 3, add the -p python3.4 flag.
RUN virtualenv /env

# Set virtualenv environment variables. This is equivalent to running
# source /env/bin/activate. This ensures the application is executed within
# the context of the virtualenv and will have access to its dependencies.
ENV VIRTUAL_ENV /env
ENV PATH /env/bin:$PATH

# Install dependencies.
ADD requirements.txt /app/requirements.txt
RUN pip install -r /app/requirements.txt

{% endhighlight %}

You’ll note that since we’re deploying our app without a database, we enable the NODB environment variable.

{% highlight bash %}

ENV NODB 1

{% endhighlight %}

Finally, we add our code and start Gunicorn:

{% highlight javascript %}

CMD export DJANGO_PASSWORD=$(cat /etc/secrets/djangouserpw); gunicorn -b :$PORT mysite.wsgi

{% endhighlight %}

You can ignore the secrets for now, as that’s to authenticate to the database, which setting the NODB flag will avoid the need for.

To build the image, you’ll need to do a docker build. On OS X, I first make sure I create a VirtualBox machine:

{% highlight bash %}

$ docker-machine create --driver virtualbox default

{% endhighlight %}

Then I start it and make sure the environment variables to create it are initialized:

{% highlight bash %}
$ docker-machine start dev
$ eval $(docker-machine env dev)
{% endhighlight %}

Finally, I build my image, tagging it appropriately

{% highlight bash %}
$ docker build -t waprin/my-guestbook-app .
{% endhighlight %}

I can then run my image locally:

{% highlight bash %}
$ docker run -p 8080:8080 waprin/my-guestbook-app
{% endhighlight %}


I get the IP of my Docker host by running:

{% highlight bash %}
$ docker-machine ip
{% endhighlight %}


Then by going to that IP, I can see my app

{% highlight bash %}

http://192.168.99.100:8080
{% endhighlight %}

# Step 3: Creating a Kubernetes Cluster 

For this tutorial, we’ll use Google’s managed Kubernetes service called Container Engine. Alternatively, you can run Kubernetes yourself on Google Compute Engine or other cloud providers like Amazon Web Services. The advantage of Container Engine is that Google manages your Kubernetes master for you, significantly simplifying the operations of a Kubernetes cluster.

To start, you’ll need to make a Google Cloud account, and create a new project using the [Cloud Console](https://console.developers.google.com). If you’re new to Google Cloud, you can sign up for a 3-month, $300 free-trial to try it out. Once you have an account, create a new project and take note of the Project ID, which is sometimes but not always the same as the name you gave the project.


<img height="300" width="600" src="{{ site.url }}/assets/console.png" />

Here kube-django-prac is the name of the Project, as well as the Project ID

Container Engine will create Google Compute Engine instances for you, and you’ll be charged for the usages of those instances

While you can create a Container Engine cluster from the Cloud Console, I prefer to you use the [gcloud command line tool](https://cloud.google.com/sdk/gcloud/).

{% highlight bash %}
gcloud components update # make sure it’s up to date
gcloud config set project <project-id>

# Create the cluster with 2 nodes
gcloud container clusters create guestbook --scopes "https://www.googleapis.com/auth/userinfo.email","cloud-platform" --num-nodes 2 

# Configure kubectl with the right context
gcloud container clusters get-credentials guestbook

{% endhighlight %}

Here we are creating 2 nodes. Note that for Container Engine, you will be billed for the instances you are creating (but for up to 5 nodes, there are no additional charges). 

When you’re done with this tutorial, to avoid recurring charges, delete the instances.

{% highlight bash %}
# Only run this when you're done the tutorial
gcloud container clusters delete guestbook
{% endhighlight %}

The main CLI to interact with the Kubernetes cluster will be kubectl. At first, the only existing Service should be Kubernetes, and you shouldn’t have any pods.

{% highlight bash %}
$ kubectl get services

$ kubectl get pods
{% endhighlight %}

# Step 4: Deploy Our App To Kubernetes 

Now that we have an application container and a Kubernetes cluster.

Finally, go back to the root directory of the repo and cd into `kubernetes_config`, which contains all the different kubernetes config. For now, we’ll focus on frontend.yaml, which stands for our Django controller.

We are creating a Replication Controller, that will create many Pods that run the image we created earlier. We specify 3 replicas to start, which means that if any container dies, our Replication Controller will replace it with a new one.

{% highlight bash %}
apiVersion: v1
kind: ReplicationController
metadata:
  name: frontend
  labels:
    name: frontend
spec:
  replicas: 3
  template:
    metadata:
      labels:
        name: frontend
    spec:
      containers:
      - name: guestbook
        # Replace  with your project ID or use `make template`
        image: waprin/my-guestbook-app 

        # This setting makes nodes pull the docker image every time before
        # starting the pod. This is useful when debugging, but should be turned
        # off in production.
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
{% endhighlight %}

The first change we have to make is to use the image we created earlier. In the repo, I’m using : gcr.io/$GCLOUD_PROJECT/guestbook, because I pushed my image to Google Container Registry, which like the public Docker registry, but private to your Google project in case you want to keep your images secret. In any case, let’s replace it with the image I created earlier:

{% highlight bash %}
docker push waprin/my-guestbook-app # replace with the image you tagged earlier
{% endhighlight %}


then in frontend.yaml 

{% highlight bash %}
# Replace with your image id in frontend.yaml
image: waprin/my-guestbook-app
{% endhighlight %}

Once the replication controller is created, we can scale it automatically or manually. The auto-scaling is a beta feature I’ll demo in a later post in this series ,but the manual scaling will be very simple:

{% highlight bash %}
$ kubectl scale rc frontend --replicas=3
{% endhighlight %}

Next you’ll notice we’re creating a Service. Since we want to expose our web application to external traffic (unlike our database our cache service we’ll introduce later), we use Type LoadBalancer to provision an HTTP Load Balancer with an external IP. This assumes that your cloud provider supports external load balancers, which both Google and Amazon do.

{% highlight bash %}
apiVersion: v1
kind: Service
metadata:
  name: frontend
  labels:
    name: frontend
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 8080
  selector:
    name: frontend
{% endhighlight %}


Once you’ve replaced the image attribute with the Docker image you pushed, let’s create the Service and Replication Controller:

{% highlight bash %}
kubectl create -f kubernetes_configs/frontend.yaml
{% endhighlight %}

The Load Balancer and external IP can take a few minutes to provision. After it’s done, when you run

{% highlight bash %}
kubectl get services
{% endhighlight %}

You should see something like:

{% highlight bash %}
$ kubectl get services


NAME CLUSTER_IP EXTERNAL_IP PORT(S) SELECTOR AGE

frontend 10.67.240.157 104.197.69.33 80/TCP name=frontend 1m

kubernetes 10.67.240.1 <none> 443/TCP <none> 10m
{% endhighlight %}


Going to the external IP in your web browser should take to your app deployed in the cloud!

However, since each instance of our application controller has it’s own version of the SQLite database and in-memory cache, the application won’t behave right until we add Postgres and Redis in the next post.

# Wrapping Up 

Please note that while I work for Google Cloud, this is not an official Google product or company statement.

If you have any problems following this tutorial, ping me on the Github issue tracker or on Twitter. The next post will go through Postgres and Redis, hope you follow along!


### (X-Posted from medium.com)
