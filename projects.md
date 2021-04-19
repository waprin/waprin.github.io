---
layout: page
permalink: /projects
---
<header class="masthead">
  <nav class="masthead-nav">
    {% for nav in site.nav %}
    <a href="{{ nav.href }}">{{ nav.name }}</a>
    {% endfor %}
  </nav>
</header>

# Projects

Like many programmers, besides my work at various full-time jobs, I have a huge graveyard of side projects. I started
programming as a kid around the year 2000, and have had "the next big idea" many times. Most
of these projects were very half-baked and belong in the graveyard, the details about them lost forever to the sands of time.
However, I thought it'd be nice to write a little more about some of other others here.

# All Night FM ([https://allnight.fm](https://allnight.fm))

This site is technically live , although traffic is mostly gone. The project
was originally named All Day I Stream but had to be renamed due to a trademark dispute. 

While it's mostly defunct now, this project had by far the most popularity of any site I've worked on, including being featured in [Rolling Stone Magazine](https://www.rollingstone.com/music/music-features/icu-worker-hosts-massive-livestream-parties-to-cope-with-covid-19-stress-986730/).

Originally, at the start of COVID, my friend had a spreadsheet tracking music livestreams that were rapidly popping up during lockdown. I was
asked to turn that spreadsheet into a website. I started out by just suggesting SquareSpace. However, we wanted to add a lot of customization,
including "Zoom parties", and featured streams, and it all became very difficult to do within SquareSpace. So I migrated it
to a Django website hosted on Google App Engine (I fell in love with Django coming from PHP in the early 2010s, and I often use GCP since I worked there for 3 years).

Moreso than the stream listings, the Zoom parties became very popular. At one point we had several with 500 attendees in a row (the max Zoom capacity). Over time though,
the enthusiasm settled down and "Zoom fatigue" settled in, and coupled with having to rename the site due to a trademark dispute, most
of the enthusiasm for the site went down. At the same time, most music livestreams converged to a few big music labels that consistently
streamed on Twitch, reducing the need for a centralized aggregator. I still keep the site up, scraping the listing from various sources, and I have
a few ideas on how I could improve the site further, but I've mostly moved onto new projects.


