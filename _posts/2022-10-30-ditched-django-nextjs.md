---
layout: post
title: Why I Ditched Django for NextJS
description: "Why I made the switch away from Python
frameworks like Django and Flask to NextJS"
categories: programming
tags: [programming, webdev, javascript, python]
---

This post is about why I stopped using the web framework Django in favor of NextJS. More broadly, it’s about why I would entirely avoid Python web frameworks, such as Flask, if you plan to serve up any HTML. While I’ve only dabbled in the Ruby community, I imagine most of my points will also apply to frameworks like Rails.

The summary is that using a language like Python or Ruby for a significant web project has increasingly gotten less reasonable over time to the point where now, in 2022, it’s getting hard to justify. By not keeping your web stack in pure Javascript, you are making your life unnecessarily difficult (as usual, we’ll include languages like Typescript as part of the Javascript ecosystem). You will almost certainly invest a bunch of time-solving problems that would be automatically solved for you if you just stuck with Javascript. 

I will provide specific examples of solving problems using Django that would have been trivially solved in NextJS.

I can only think of two valid reasons to use Python or Ruby for the web in 2022:

- You’re working on an existing project that hasn’t been migrated yet or is not worth migrating.
- You are already a master of a Python or Ruby web stack, and you need to implement a new project as soon as possible, and you don’t have time to learn a better stack.

Developer circles have a sentiment that it’s best to master a few tools, know them well, and stick with them. It’s good advice to avoid constantly chasing new tools and frameworks over getting any work done. The developers I know who are best at shipping things have a few solid tools they stick with and focus on shipping products rather than updating their tech stacks. 

But, like many pieces of advice, the truth is that you need to find a balance. YCombinator founder Paul Graham wrote at length about how startups were finding competitive advantages via DevEx in the web2 era by picking productive languages like Ruby and Python over more traditional languages like Java and C++. Avoiding new tools at the extreme turns you into a Luddite, and you will not be able to keep up with the pace of modern technology.

While my first few jobs out of college were Java and C++, I fell in love with how productive and "batteries included" Django was and switched my side project stack from PHP to Django. I pushed to work on Python and Django and when I joined Google I led all the documentation around using Django on Google Cloud Platform, including docs on how to run it on App Engine (managed and flexible), Compute Engine, and Kubernetes / Container engine. My only Github repo that's attracted non-negligible attention is a [Django on Kubernetes sample](https://github.com/waprin/kubernetes_django_postgres_redis). And in past few years the vast majority of my development focus has been on Python.

So I was not eager to get rid of Python, if anything my career has me tagged as a “Python guy”. In 2020, my non-technical friend really wanted to make a little side project where we listed music livestreams and hosted Zoom parties around them. We felt there was a cultural wave as part of Covid and wanted to move fast so I stuck with what I knew which was Django. In some sense it worked really well because I had several non-technical people use the admin console to update the website with minimal influence from me.

The issue is that I ran into several problems:

- At first, I thought I didn’t need fancy frameworks like React, and it’s better to use something simple, which was [ZeptoJS](https://zeptojs.com/) (a more perfomant jQuery clone). But even the “simple” features our website needed like an infinite scroll of music livestreams started turning into spaghetti code. I wanted to move to React to achieve a more declarative approach but getting Django and React to play nicely together was non-trivial. NextJS makes it trivial to start a new React project, and even brings me back to the PHP days of mapping the filename to a single page
- My webpage loaded a bunch of images and rendered them in a gallery which was very slow. I wanted to only load the image when the user scrolled to see it. To accomplish this, I had to use the [Intersection API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API), which was fun, but [NextJS Image](https://nextjs.org/docs/api-reference/next/image) component does this out of the box.
- Because I wanted infinite scroll to make the website more modern, I had to render the grid components as they scrolled. It would have been better to do this server-side since it would be faster, but it also needed to be done client-side after the timezone was updated. (see my post on
[How to show local timezones on a webpage without asking the user for their location
](http://billprin.com/2020/05/12/local-timezones.html))
- Furthermore, I  wanted the first page load to be very quick and contain content so the SEO would be faster. Some of the content could be rendered ahead of statically. But again, I had to rewrite the same code in Python and in Javascript

So one of my biggest problem was wanting to render the same component, but some times statically ahead of time, sometimes dynamically on the server (for user specific cases), and sometimes on the client (to re-render any timezone updates). 

Being able to easily render components statically, server-side, or client-side is one of the fundamental features of NextJS. This is in addition to a ton of commonly used frontend optimizations like Image viewport rendering that Django simply does not offer. Django is not really “batteries included” anymore now that the batteries have changed.

Besides these features, there’s a few other good reasons to stick with Javascript. For one, every web project uses it so almost all of the good tooling for other things you need such as CSS preprocessing will be Javascript-centric. You will inevitably need NodeJS in your project , and if you have two languages, now you need to worry about tooling for both (e.g. dependency upgrades).

When NodeJS first came out, Python still felt a lot more usable in many ways. NodeJS would easily turn into callback hell. But in 2022, it’s Python that feels is cobbled by an awkward async story, while NodeJS async/await feels much simpler. Typescript also feels more fleshed out than Python typing and the tooling around it again feels easier to understand.

Python is still an amazing language and it’s still probably the best “jack-of-all trades” language there is. It might make sense to use something like Django Rest Framework if you plan to do a significant amount of machine learning and want to use one language to write all your models. Of course, I’m very indebted to all the amazing OSS contributions made by the Python and Django communities.

But going forward, Django is something I will look back fondly on rather than use for any projects.  Going forward, aside from quick experiments for learning purposes, I plan to stick entirely within the Javascript ecosystem for web projects.