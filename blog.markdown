---
layout: page
permalink: /blog/
---
<header class="masthead">
  <nav class="masthead-nav">
    {% for nav in site.nav %}
    <a href="{{ nav.href }}">{{ nav.name }}</a>
    {% endfor %}
  </nav>
</header>
<div class="content list">
{% if site.posts.size == 0 %}
  <h2>No post found</h2>
{% else %}


  <h3>Medium </h3>

<div class="list-item">
<a href="https://medium.com/google-cloud/a-tensorflow-glossary-cheat-sheet-382583b22932"> A TensorFlow Glossary/Cheat Sheet</a>
    <div class="list-post-date">
    August 29, 2017
  </div>
</div>  

<div class="list-item">
    <a href="https://medium.com/google-cloud/local-django-on-kubernetes-with-minikube-89f5ad100378">Local Django on Kubernetes with Minikube</a>
  <div class="list-post-date">
    December 13, 2016
  </div>
</div>


<div class="list-item">
    <a href="https://medium.com/google-cloud/deploying-django-postgres-and-redis-containers-to-kubernetes-part-2-b287f7970a33#.ynn5h3jme">Deploying Django to Kubernetes (pt2) </a>
  <div class="list-post-date">
    March 31, 2016
  </div>
</div>

<div class="list-item">
    <a href="https://medium.com/google-cloud/scalable-video-transcoding-with-app-engine-flexible-621f6e7fdf56">Scalable Video Transcoding with App Engine Flexible </a>
  <div class="list-post-date">
    Aug 8, 2016
  </div>
</div>

  
  <h3>Google Cloud Blog</h3>
  
<div class="list-item">
  <a href="https://cloud.google.com/blog/big-data/2017/11/using-apache-spark-with-tensorflow-on-google-cloud-platform">Using Apache Spark with TensorFlow on Google Cloud Platform </a>
    <div class="list-post-date">
   November 28, 2017
  </div>
</div>




<div class="list-item">
    <a href="https://cloud.google.com/blog/big-data/2017/04/deepbreath-preventing-angry-emails-with-machine-learning">DeepBreath: Preventing angry emails with machine learning (Google Cloud ML Blog)</a>
  <div class="list-post-date">
    April 6, 2017
  </div>
</div>

<h3>This Site</h3>

{% for post in site.posts %}
  <div class="list-item">
      <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
    <div class="list-post-date">
      <time>{{ post.date | date_to_string }}</time>
    </div>
  </div>
{% endfor %}
  

{% endif %}
</div>
