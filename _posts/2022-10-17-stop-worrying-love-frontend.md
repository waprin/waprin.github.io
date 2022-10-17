---
layout: post
title: How To Stop Worrying And Love Frontend Dev
description: "comparing frontend vs backend career options"
categories: programming
tags: [programming, frontend]
---

This blog post is intended for a specific type of software engineer. It’s a type of engineer that I used to be. An engineer who’s been brainwashed into thinking frontend development is somehow “inferior” to backend dev.

In the past I’ve had thoughts like: 

- Frontend is cool, but real computer science and engineering lives in the backend
- Frontend is cool, but the work is too commoditized by cheap offshore contractors and “bootcampers”
- Frontend is cool, but the big and new opportunities are in more cutting-edge spaces like machine learning / AI , distributed systems, and blockchain

All three of these thoughts are absolutely wrong. There’s tons of computer science in frontend dev. There’s more money in general in frontend dev. And there’s more opportunities in general if you have frontend dev skills. I’ll delve deep into all these topics.

Because I enjoy writing long form blog posts and will go on a few tangents, I also want to place a key point at the top:

- You can enjoy learning about low level programming languages like, C, C++, and Rust, low level Linux concepts, compilers, machine learning, etc, as well as computer science topics like graphs and algorithms, and you can be relatively good at all these things, and *still* focus your career more on frontend dev *if thats what you want to do*.
- And of course, focus on Rust , C++, Haskell or x86 *if thats what you want to do*

_Do what you want to do_ sounds like obvious advice, but it’s not when the world keeps hinting that you’re silly for wanting to do that. I had thoughts that frontend was somehow not how the best of use my time if I happened to also think low level programming and computer science were also fun. 

It’s no surprise I had those thoughts. They were reinforced at almost all my jobs. 

At one my second job out of college, I was at startup where my primary role was to write C++ for low-latency scrapers. Meanwhile, my coworker was building a frontend in this brand new technology called NodeJS. Javascript, on the server? I was intrigued. I asked my management if I could spend a little time helping my coworker with the NodeJS project, which they gracefully agreed to. This experience ended up saving the company during Hurricane Sandy . (footnote 1)

But at my next company during the interview, I remember telling this story and being told, that by the interviewer that by asking to work on a frontend project, I was “asking for a demotion”. 

The idea that frontend dev is “lower” than backend dev is an attitude that was frequently reinforced at Google. During orientation I was told by the instructor, Google has 4 main languages: “C++ because we hire real engineers, Java because we hire a lot of college students, Python for little scripts, and Go because we hired Rob Pike. Oh, and Javascript for the frontend devs”. In this instructor’s view, only C++ work deserved the badge of “real” engineering.

I’m not saying *everyone* insists that the more low level your programming language is, the more you’re a “real” engineer. But I do think if you spend time in the engineering side of the tech industry, you’ll encounter this concept. Even though it’s a really dumb and completely incorrect concept.

## A brief history of my early programming adventures

I myself admit to having this bias. Part of the problem is that it used to be true that you need to use a “real” language to build any sort of product that you could actually ship.

Like many developers, I got interested in programming to make games. Specifically [MUDs.](https://en.wikipedia.org/wiki/MUD) I was an unpopular middle schooler who got obsessed with Dungeons & Dragons, but I only had the player’s manual and no friends to play with. Plus my parents and teachers were convinced it was satanic. I then learned that people were playing this game in virtual worlds over Telnet. To say I became hooked was an understatement. Ironically, I never got addicted to later MMOs like World of Warcraft because the gameplay and social experiences of modern MMOs seemed so shallow compared to these amazing text-based worlds. 

The MUDs had a hierarchy. At the bottom of the hierarchy were the players who just played the game. Above them were two levels of “immortals” who built the game, the builders and the coders. The builders would write the room descriptions (e.g. “You’re in a dark cavern, the stalactites stick out like the bones of an ancient beast, and the groans of distant disturbances echo off the moist stone walls. You can move north, west, or east.”). I quickly became a builder. But the *real* cool people were the coders. They were the people who actually created the MUDs. 

Pretty much every MUD engine that was important like DikuMUD and CircleMUD were written in C. These engines were written at a time when Python barely even existed. Languages like Perl were popular but were not a realistic choice to build an engine that could handle multiple connections. So if you wanted to be the coolest kid on the server, you had to learn C. When I was 14 I worked all summer as a dishwasher making $5.75 an hour and my prize purchases were a shortboard surfboard and a copy of K&R (still have both, and my K&R is signed).  

Why do I think this story about MUDs is relevant? Because if I told you I was eager to learn C as a young child you might mistakenly think I was super motivated to learn about low level programming concepts. **When really my motivation was to make cool stuff that I could share with other people, most of whom could not read code themselves.**

But I foolishly thought that because I _knew_ C++ well when I graduated college, it would be beneath me to focus on Javascript instead. How wrong I was!

## The web in 2022

The MUD era was the late 90s. Browsers were a lot more limited. Javascript existed but it mostly was used just to jigger some things around the screen, there weren’t many “web apps”. Of course, the popularization of AJAX was the major turning point in “apps” emerging in the web, but there’s also been major improvements in the hardware speed of typical consumer devices, browser performance, the Javascript language & ecosystem, and available web APIs.

There’s also hybrid “frontend with backend” language options available like writing Rust and compiling it down to WebASM but that still seems pretty niche. Let’s just focus on Javascript (and Typescript) . Typescript has taken over the world and I’m all aboard but I’ll just use the term Javascript for simplicity to capture the whole ecosystem.

If your motivation is to make cool stuff that you can share with other people who don’t code, you are much better off being a Javascript expert than a C++ expert. In the 90s, C++ would be a popular option for a desktop app. Nowadays, people don’t even use many desktop apps and if they do, they’re probably written in Swift, C#, or ….Javascript.

What if you’re really passionate about computer science? Shouldn’t you focus on backend? I would again argue no. There’s plenty of computer science in the frontend , arguably more. Having worked at some of the big Silicon Valley companies and having friends at most of them, most of the backend work at these companies is a lot of boilerplate Java where you move JSON / protobufs / thrift structs around. There’s a bunch of imperative API microservices that do so. I’ve seen a bunch of companies adopt Scala and basically write “Java with a tiny bit of Scala and using pattern matching instead of `if` statements to feel functional”.

Meanwhile, React is the most popular frontend framework and clearly heavily inspired by functional programming, especially since the move away from class based components to functional components. The new hot iOS dev framework is SwiftUI which is very similar to React in its functional approach of composing views based on state updates. 

There’s also compiler projects like Babel, that compile new versions of Javascript down to old ones for browser compatibility.  There’s computer graphics projects like [ThreeJS](https://threejs.org/) that run advanced 3D rendering algorithms on the browser.

Frontend is filled with computer science. Really, most programming is, other than the typical type of API / microservices drugergy most generic backend devs get shuffled into. My current biggest focus is called Navigoals and is basically a habit tracker taken to the next level. One major concept is representing your habits as a [directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph). The reason for doing this is so that you can increment a habit but then have it count towards several parent habits / tags, then be able to do analytics on how you spend your time at a more fine-grained level than if you simply used groups or basic tags. 

Below is an example Habit DAG, (Navigoals the goal tracker and Slime Volleyball 3.0 is a  hypothetical indie game).


<img height="300" width="500" src="{{ site.url }}/assets/habit_dag.png" />

If you want to answer questions about how you much time you spent coding or on
a given project you do a Depth-First Search from the parent habit to all
children habits. And this is in one of the simplest possible projects imaginable - a habit tracker!

## The financial opportunities in frontend dev

Let’s switch to one of everyone’s favorite topic - money.

If you just want to go for the most obvious way to make money as a programmer, that would be getting full time job at a company. In big tech, I’d estimate there are about equal amount of opportunities focusing on the frontend or on the backend. The backend engineers may talk down on frontend engineers, But as mentioned, there’s still tons of computer science in the frontend. Frontend in 2022 is not 2005, companies need sophisticated web applications and they need strong engineers to build them. So almost every big tech company I know uses the same compensation system for frontend as it does backend.

In fact, as much as people think web dev is commodotized, in my experience it's 
a less common skill amongst people who are actually good at computer science. Many CS graduates avoid webdev and focus on topics like machine learning and distributed systems as well, so if you want to find someone who has excellent CS fundamentals _and_ isn't terrified by the thought of CSS, it can be slim pickings.

Not only that , but only a handful of companies truly value their backend and infrastructure engineers. I’ll concede that Google certainly does , but Google’s one of the exceptions, not the rules. In general, to make money as an employee, you want to be working at a “profit center” not a “cost center”. Most companies have leadership that see their software products being made and assume the people making the part of the product they actually see are making the profits. The infrastructure engineers are basically the same as IT. Google was founded by 2 Computer Science PhDs so does not operate this way. If your company is founded by Computer Science PhDs this rule of thumb might not apply. Most are not.

There’s also an idea that “bootcampers” and cheap offshore labor can do frontend and by doing backend you have more job security. I think it’s true that bootcampers and offshore contractors learn frontend but that’s because they know there's a very strong market demand, and **demand is what makes a job well paid, not difficulty.**

There’s this weird idea I see sometimes that because embedded programming is “hard” or distributed systems are “hard” , people will pay more for it. That’s only true if the difficulty leads to lower supply of people. But compensation is based on supply & demand and a lot more companies tend to need web devs than embedded engineers. 

Software engineer compensation really exploded in the 2010s which was reflective of explosion in consumer apps like AirBnB and Uber. Certainly those apps have a ton of both frontend and backend work, but the point being is that areas like embedded engineering were around for many years and not especially well paid. Even if, unlike me, you’re convinced lower level engineering is more difficult, that has almost nothing to do with how lucrative it is.

It’s true that if you’re one of the best machine learning engineers in the world, a leading researcher, then companies like Google and Facebook will pay more for you than a frontend dev. But if you’re a leading researcher in machine learning, you know you want to do machine learning, you don’t need any convincing one way or the other. 

Even if you *are a* world class deep learning researcher, even they know the benefits of frontend. One of the most interesting people on the internet, who I already discussed in my Slime Volleyball blog post, is [hardmaru](https://twitter.com/hardmaru?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor),  a deep learning researcher at Google Brain. In my older post I mentioned how he uses Slime Volleyball as a demo, and he also had a tweet to a talk where he mentioned that one of the best ways to communicate your machine learning researcher is visually. And that’s why he recommends people learn Javascript to do so, to code up algorithms visually. It’s not a coincidence [his website is filled with Javascript demos](https://otoro.net/pendulum/03/).


## What it means to be world class

On average, though, you the reader, are not a world class deep learning researcher. Maybe you know some deep learning and you’re good at it, but you’re not world class. How do people become world class at something? But how do you become world class at something? Certainly there’s a combination of talent, hard work, and opportunity. Many would argue hard work is the most important part of the formula. 

It’s possible to work hard on something you’re not particularly motivated to do, but it’s so much easier to just work hard on something that you actually want to do. Throughout my career, I had a huge hint that what I really wanted to do was frontend dev. The hint was, *all my side projects were frontend project*.

Even though I insisted on getting a C++ job out of school, I synced up with someone who was still an undergrad to make a website that filled in some of Facebook’s college-focused features they had removed between 2004 and 2009 as they broadened to a wider audience (e.g. sharing resources and review for a specific class). In 2014 I took a break from my job and learned Django so I could make an analytics app for my fantasy football team. In 2020, my friends and I got excited to work on app that listed all the music livestreams for DJs so we could host Zoom dance parties for them.

During the day job at my career, I’ve only dabbled in frontend when the opportunities have come up. At a few points I’ve tried to nudge myself closer, but I’ve equally nudged myself away when I decided once again that "real" engineers should focus on distributed systems or "real" engineer should focus on machine learning.

These days, I’m happy to be focusing on frontend, both web and mobile. The developer experience for Typescript with NextJS, Firebase, and TailwindCSS is just so ***fun***. And Swift is currently my favorite language and SwiftUI with XCode is equally a blast. Infinitely more fun than any developer experience I’ve had on the backend. Good developer experience makes me happy and productive. And you're not going to do world class work unless you're happy
and productive.

## Even more financial opportunities for frontend devs

 As you may have picked up from me, I don’t appreciate being pigeonholed into a box: see ( I am not a “[Javascript Developer](https://andrewkelley.me/post/not-a-js-developer.html)” by Andrew Kelley, the creator of the Zig language). 
 Recruiters always message me, "hey - do you want to do exactly what you've been doing recently, except probably for less money" - no thanks!

 I’m massively inspired by the Indie Hacker community as a way to get variety without having to beg for variety from my manager or beg for money from venture capitalists. Besides my project Navigoals, I’m researching all sorts of ways I can make money online with software skills.

But if you scroll through Indie Hackers, you’ll notice that pretty much every single opportunity is frontend focused. There’s exception, especially if you can look for ways to sell stuff *about* backend rather than backend itself, such as books or courses on AWS. But on the whole, if you want to do indie hacking stuff, you’re far, far better off knowing Javascript than C++.

It’s true that on average, Indie Hackers make a **lot* less than BigTech SWEs do. A *lot* less. Senior at BigTech is usually 400k, Staff is 600k, even startups can usually get you to 200k base. Indie hackers often celebrate 20k for the entire year, which would be a small signing bonus to BigTech SWEs. The catch is that indie hackers have way more upside. By owning their own businesses, if they ever do find a breakout success, they can make tens or hundreds of millions of dollars. Silicon Valley likes to give engineers the illusion of that possibility , but it’s almost always an illusion, except for a rare few who win the startup lottery (and even then, VCs have extracted most of the value out of ISOs and most IC engineers get too small a percentage to matter).

More importantly than money, indie hacking is usually a lot more *fun* than IC BigTech or VC startups. But the financial potential is on average lower but potentially much higher.

Even if you want to do a VC-backed startup, you’re *still* often better off doing frontend. The biggest crypto YC successs stories are Coinbase and OpenSea and both their MVPs involved a lot more frontend work than backend work. I was recently at a San Francisco crypto meetup and spoke with the founders of the Solana Phantom wallet, which raised $100M at a $1B valuation, and their CEO told me he coded most of the product but never wrote a single smart contract in Rust, the programming language for Solana. He simply didn’t need to, an didn’t want to distract himself, cause his core product was the Chrome extension , written in Javascript.

## Conclusion

Before my grandmother died, often times she would reply to pretty much any conversation with *“do what makes you happy”*, which she said in a voice that was a funny combination of an old Brooklyn accent and her aging vocal cords. Nowadays, when my family discusses any scenario where someone solicits any sort of advice, usually someone imitates the grandma voice and says “*do what makes you happy”*.

If low-level C++ and Rust makes you happy, do that. If cool machine learning with PyTorch and numpy makes you happy, do that. If hardware and robotics and embedded programming makes you happy, do that.

But if you want to do frontend, do frontend. And if a backend elitist ever condescends to you about it, dismiss their foolish opinion and laugh internally at their ignorance. Because doing frontend can expose you to lots of cool computer science concepts, it can make you lots of money, it lets you build products that you can share with anyone. Most importantly, it can even make you happy.

1) How my exposure to frontend saved the startup. During Hurricane Sandy, there was a major AWS outage. I was also the only engineer the company with power. I had to rebuild our entire infrastructure by myself, which I was only able to do because my manager let his C++ engineer mess around with the frontend stack for a couple month