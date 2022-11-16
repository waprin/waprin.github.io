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

# Navigoals (coming soon)

This is an advanced goal, habit, and time tracker for people who want to track everything aka "the quantified self". It makes it easy to roll up habits into a tree (really, a directed acyclic graph) to
have a more nuanced view of how you spend your time. I use it to set high level goals like "be productive",
then use the Pomodoro technique to track work on multiple different projects towards those goals.

This is my centralized aggregator for tracking - for example, I use MyFitnessPal for food tracking, but
track that I used MyFitnessPal in Navigoals. I use Notion for daily planning, but track that I did
the planning and reviewed the plan at the end of the night in Navigoals. I find this really helpful
for staying on top of balancing taking care of myself with making forward progress on my goals.

Currently signups are closed but you can add yourself to the waiting list on the landing page - [Navigoals.com](https://navigoals.com).

# All Day I Stream (defunct) 

This site hosted live music livestreams and was featured in [Rolling Stone Magazine](https://www.rollingstone.com/music/music-features/icu-worker-hosts-massive-livestream-parties-to-cope-with-covid-19-stress-986730/).

Originally, at the start of COVID, my friend had a spreadsheet tracking music livestreams that were rapidly popping up during lockdown. I was
asked to turn that spreadsheet into a website. I started out by just suggesting SquareSpace. However, we wanted to add a lot of customization,
including "Zoom parties", and featured streams, and it all became very difficult to do within SquareSpace. So I migrated it
to a Django website hosted on Google App Engine.

Moreso than the stream listings, the Zoom parties became very popular. At one point we had several with 500 attendees in a row (the max Zoom capacity). Over time though,
the enthusiasm settled down and "Zoom fatigue" settled in, and coupled with having to rename the site due to a trademark dispute, most
of the enthusiasm for the site went down. At the same time, most music livestreams converged to a few big music labels that consistently
streamed on Twitch, reducing the need for a centralized aggregator. 

