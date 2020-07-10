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
<a class="social" href="http://linkedin.com/in/{{ site.author.linkedin }}"><i class="fa fa-linkedin"></i></a>
<a class="social" href="http://github.com/{{ site.author.github }}"><i class="fa fa-github"></i></a>
<a class="social" href="http://stackoverflow.com/users/{{ site.author.stackoverflow }}/"><i class="fa fa-stack-overflow"></i></a>
<a class="social" href="https://medium.com/@{{ site.author.medium }}"><i class="fa fa-medium"></i></a>

<img height="300" width="300" style="float: right;" src=
"{{ site.url }}/assets/waprin_profile.jpg" />

<br />

Hi, my name is Bill, and I'm a Software Engineer living in San Francisco.

During the day, I work at an RF startup called Bastille, building data pipelines in Python. Previously, I worked
at Google building machine learning pipelines to analyze mobile developer tools. Before that at Googe, I worked
 on Google Cloud Platform developer relations building sample apps and client libraries. I also spent several 
 years working at NYC startups after graduating with a Computer Science degree from Johns Hopkins University.
 
 
My most recent side project is [All Night FM](https://allnight.fm), a COVID inspired tracker for music livestreams
and associated Zoom parties. You can find some other defunct projects on my Github repositories.

You can click on the relevant social media links above for more information about me, including my LinkedIn, GitHub,
and StackOverflow. The blog page contains some links to articles on this site and some external links.

On weekends, you might find me surfing at Linda Mar in Pacifica or snowboarding at Northstar or Kirkwood in Tahoe. I love music,
especially electronic music, and dabble in producing it, which you can check out on [my SoundCloud](https://soundcloud.com/metawish).
