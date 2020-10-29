---
layout: page
permalink: /
---
<header class="masthead">
  <nav class="masthead-nav">
    {% for nav in site.nav %}
      <a href="{{ nav.href }}">{{ nav.name }}</a>
    {% endfor %}
  </nav>
</header>
<a class="social" href="https://twitter.com/{{ site.author.twitter }}/" target="_blank"><i class="fa fa-twitter"></i></a>
<a class="social" href="http://linkedin.com/in/{{ site.author.linkedin }}"><i class="fa fa-linkedin"></i></a>
<a class="social" href="http://github.com/{{ site.author.github }}"><i class="fa fa-github"></i></a>
<a class="social" href="http://stackoverflow.com/users/{{ site.author.stackoverflow }}/"><i class="fa fa-stack-overflow"></i></a>
<a class="social" href="https://medium.com/@{{ site.author.medium }}"><i class="fa fa-medium"></i></a>

<h1>Welcome To Bill Prin's Personal Site</h1>

<div class="intro">

<div class="intro-text">    
<p>Hi, my name is Bill Prin. My legal name is William Prin, hence the initialization "waprin" that I use
as an online professional alias, including this website's URL ('A' is my middle initial). 

I realize that many people don't always realize that William shortens to Bill, especially international people, it 
doesn't make sense to me either - blame my parents :) ! </p>

<p>
I am a software engineer living in the beautiful city of San Francisco, California. You can learn a
little more about me by clicking on the "About" link above. I also occasionally write (mostly) technical 
blog posts, some for employers, and many "just for fun"! They are linked below, with some hosted on this site
and some external links.
</p>

<p>
The icons above also link to many of professioanl and social media presences.
</p>
</div>

<div class="intro-pic">
<img height="300" width="300" src="{{ site.url }}/assets/waprin_profile.jpg" />
</div>

</div>


<h2>Technical Blog</h2>
<div class="content list">

{% for post in site.posts %}
  <div class="list-item">
     {% if post.external_url %}
     <a href="{{ post.external_url }}">{{ post.title }}</a> ( {{ post.external_site }} )
     {% else %}
      <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
     {% endif %}
    <div class="list-post-date">
      <time>{{ post.date | date_to_string }}</time>
    </div>
  </div>
{% endfor %}

</div>
