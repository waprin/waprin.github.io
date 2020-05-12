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
