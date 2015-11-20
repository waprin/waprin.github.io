---
layout: post
title: A Simple Tox Tutorial
description: ""
categories: tech
tags: [python, tox, tech]
---

## Tox, The Python Test Automation Framework

A while back, I noticed a lot of Python projects were starting to contain a file called 'tox.ini', which is
  a file read by [tox](https://tox.readthedocs.org/en/latest/). 
   
Of course, the tox documentation should be considered the canonical source. 
It has lots of good examples, but I still found the docs a bit confusing at 
first, so I thought I would take my own shot at explaining the basics.   
   
   This is what a complete tox.ini file might look like:
   
   {% highlight java %}
   [tox]
   envlist = py26-django{15,16},
             py{27,33,34}-django{15,16,17,18}
   install_command = pip install {opts} {packages}
   
[testenv]
   basepython =
       py26: python2.6
       py27: python2.7
       py33: python3.3
       py34: python3.4
   
   commands =
       nosetests

   deps =
       nose
       django15: Django>=1.5,<1.6
       django16: Django>=1.6,<1.7
       django17: Django>=1.7,<1.8
       django18: Django>=1.8,<1.9
   {% endhighlight %}
   
   
   At first, it was unclear to me what the point was at all, because we were 
   already either using unittest 
   or nose to actually run the tests. If we already have a test framework,
   why do we need yet another tool?

The problem that tox is trying to solve is that your tests might be run using
 multiple tools in a variety of different environments. So, for example, you might want to run
 Python unit tests using the standard unittest tool, as well as check your 
 style with a tool like flake8, and your code coverage with a tool like 
 coveralls. You want to run these tools using both Python 2.7 and Python 3. 
 That means you have 3 different 
 tools and 2 different environments.
 Tox helps you declare how all of this gets pieced together in one spot, and 
 helps manage situations like different environments requiring different 
 dependencies.
  
This combination of environments is generally what you specify at the top of 
the tox file underneath the [tox] directive, like so:

{% highlight java %}
[tox]
envlist = py26-django{15,16},
          py{27,33,34}-django{15,16,17, 18}
{% endhighlight %}

In the above example, we are creating 14 different environment names, 2 
environments on the first 
line and 12
environments on the second line. Using the braces means we want to repeat 
each of the *factors* in the braces for a different environment. So the first
 line 
creates two environments, py26-django15 and py26-django16. The second line 
creates 12 more environments, combining each of the three versions of Python 
that we specify with each of the 4 different versions of Django that we specify.

Following that, we can put all our default settings that applies to all 
environments underneath the [testenv] directive: 

{% highlight java %}
[testenv]
  configuration that applies to every environment goes here
{% endhighlight %}

Next, we configure specific environments by adding a a directive with the 
environment name after the colon, so to 
setup configuration specific to the Python 2.6/Django1.5 environment we created 
above we would add:

{% highlight java %}
[testenv:py26-django15]
{% endhighlight %}

and then we would put everything specific to that environment underneath it.

Until we configure an environment, it's doesn't have any special meaning. 
py26-django15 is just a name 
until we use 
the basepython directive to match  the py26 "factor" to the python2.6 
executable, and the deps command to match django15 "factor" to the Django1.5 
dependency. 

Here is how we can match our Python environment names to the correct Python executable: 

{% highlight java %}
[testenv]
basepython =
    py26: python2.6
    py27: python2.7
    py33: python3.3
    py34: python3.4
{% endhighlight %}    

Note how we are individually referencing just part of the environment name 
, or factor, such as py26, and tox is smart enough to match that base command 
with all the complete environment names that contain the  py26 factor.

We also need to add the correct dependencies, which we might do something 
like this:

{% highlight java %}
deps =
    pytest
    django15: Django>=1.5,<1.6
    django16: Django>=1.6,<1.7
    django17: Django>=1.7,<1.8
    django18: Django>=1.8,<1.9
    py26: unittest2
{% endhighlight java %}    

My first question upon seeing the deps field in tox was, why are we using tox
 to manage dependencies? I thought the general Python best practice was to 
 combine a requirements.txt file with something like pip?
 
 While pip is a  popular approaches to dependency management, it's not 
 the only ones, and tox tries to remain somewhat agnostic and not rely on pip
  or the existence of a requirements.txt
. However, if your dependencies are nicely captured in a requirements.txt 
 file, tox supports that:
 
{% highlight java %}
 deps = -rrequirements.txt
{% endhighlight %} 

Finally, we need to give tox something to actually run our commands. This is 
literally just the command we need to run, so it's something as simple as:

{% highlight java %}
commands =
    python test.py
{% endhighlight %}

With all this done, we can just run 'tox' and all our commands will be run 
for each of our environments.

## I'll Be Back (with something else)

So that's a basic introduction to tox and why you would use it. A lot of this
 information is a rehash from the tox documentation, and of course the best 
 way to learn is by example, for which you can find many on the tox site and 
 floating around on Github. The Google Cloud Devrel team plans to use tox to 
 automate much of our testing work, especially since we are trying to 
 improve the automated testing of our sample code, so you can check out our 
 usages of tox in any Python repo on our [Github organization](http://github.com/GoogleCloudPlatform).


> "Every man is a poet"
> -- *Post Office, Charles Bukowski*
