---
layout: page
permalink: /about
---
<header class="masthead">
  <nav class="masthead-nav">
    {% for nav in site.nav %}
    <a href="{{ nav.href }}">{{ nav.name }}</a>
    {% endfor %}
  </nav>
</header>
<a class="social" href="https://twitter.com/{{ site.author.twitter }}/" target="_blank"><i class="fa fa-twitter"></i></a>
<a class="social" href="http://linkedin.com/in/{{ site.author.linkedin }}" target="_blank"><i class="fa fa-linkedin"></i></a>
<a class="social" href="http://github.com/{{ site.author.github }}" target="_blank"><i class="fa fa-github"></i></a>
<a class="social" href="http://stackoverflow.com/users/{{ site.author.stackoverflow }}/" target="_blank"><i class="fa fa-stack-overflow"></i></a>
<a class="social" href="https://medium.com/@{{ site.author.medium }}" target="_blank"><i class="fa fa-medium"></i></a>

<img height="300" width="300" style="float: right;" src=
"{{ site.url }}/assets/waprin_profile.jpg" />

<br />

Hi, my name is Bill, and I'm a Software Engineer living in San Francisco.

I currently work at Thumbtack, leading their "Growth Platform" efforts, building out data and machine learning platforms 
for marketing and analytics, and bridging the gap between data engineering, machine learning engineering, and 
marketing teams.  


# About This Site

This site is a static page made with Jekyll served on Github pages.