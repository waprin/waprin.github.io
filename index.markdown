---
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

<img height="300" width="300" style="float: right;" src=
"{{ site.url }}/assets/waprin_profile.jpg" />

Hi, my name is Bill, and I'm a Software Engineer living in San Francisco.

You can click on the relevant social media links above for more information about me, including my LinkedIn, GitHub,
and StackOverflow. The blog page contains some links to articles on this site and some external links.

On weekends, you might find me surfing at Linda Mar in Pacifica or snowboarding at Northstar or Kirkwood in Tahoe. I love music,
especially electronic music, and dabble in producing it, which you can check out on [my SoundCloud](https://soundcloud.com/metawish).



[Jekyll theme](https://github.com/gfjaru/Kiko) courtsey of [gjfaru](https://twitter.com/gfjaru).
