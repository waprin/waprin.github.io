---
layout: post
title: The Simplest App That Makes Money
description: "Making the simplest app that makes money, an Apple Watch app for poker players"
categories: startups
tags: [bootstrapping, startups, ios]
---

<div style="margin:auto; width: 400px;" >
<img  height="200" width="200" src=
"{{ site.url }}/assets/money_on_mind.jpeg" />
</div>

This blog post is about a simple goal and exercise I went through this November. The exercise was:

*In one month, starting from scratch, create a new app that a stranger pays for by the end of the month.*

I succeeded at this goal, but only by a hair - I sold two In-App Purchases for $19.99 each. While this is a modest achievement, I still feel proud that I succeeded at a simple goal. These two sales came from a single Reddit post that was eventually removed for self-promotion. If a single post can get any sales, more marketing efforts and product improvements can probably generate more.


<img height="400" width="400" src=
"{{ site.url }}/assets/app_sales.png" />

(Apple shows that I have ~$80 in sales rather than ~$40, because $40 came from my own test purchases)

While some developers struggle to ideate new concepts, I’m one of those developers with too many ideas. I have a Notion list with hundreds tagged by category. My constraint of wanting to sell the software to a consumer after only a few weeks of work added a simple and helpful filter:

**Make The Simplest App That Makes Money**

This filter narrowed hundreds of ideas down to only a few.

Ultimately, the app that I made is unlikely to be a long-term business. It targets a niche of a niche market - poker players who own Apple Watches. 

Still, to me there’s value in making even a tiny amount of money. It got me experience in working with APIs like In-App Payments on Apple which will be critical to make any money in the Apple ecosystem. 

Due to the [Matthew effect](https://en.wikipedia.org/wiki/Matthew_effect), there’s an aspect to life and startups where “winners keep winning”. That’s why it’s important to find small wins because they tend to compound on each other. Any income at all also extends my entrepreneurial runway.

To the extent there’s more online opportunity in b2b market, I’m hypothesizing one of the best ways to discover them is to actually create online businesses. But if your app is free with no revenue, it’s more of a hobby than a business. Since I have an app at least some people will pay money for, it makes
more sense to explore options like paid ads and running experiments around optimizing RoaS (return-on-ad-spend), something I've done before as an engineer on Growth teams for Silicon Valley companies.

Finally, as someone blogging about my experience indie hacking / bootstrapping, making any money makes me a more interesting storyteller than someone with a big fat 0 in the revenue column.

### How I Selected the App

In general, it’s tough to quickly make money in any space that’s super crowded. While the biggest upside exists in general consumer markets, it’s also where you face the toughest competition from both established companies and many other upstarts with the same idea.

Microconf founder Rob Walling discusses the value of pursuing niches in his book *Start Small, Stay Small.* Niches won’t have much competition from big companies since the market opportunity is too small. Niches will be cheaper to market too since you can buy ads on more small, focused communities. 

This raises the question - how do you select a niche? There’s a few strategies here - some people like analyzing Reddit or Twitter for small but growing new trends. This might work, but I don’t love this approach because you won’t have any personal connection to the problem space, making it more difficult to truly build the right thing and stay motivated.

One of my favorite entrepreneurship books that I’ve recently read is *The Embedded Entrepreneur* by Arvid Kahl. Arvid stresses the importance of building for audiences that you have an affinity for. He challenges the reader to go through an exercise where you list all the audiences you are a part of, then write down how much business opportunity there might be in the space. 

<img height="600" width="600" src=
"{{ site.url }}/assets/arvid_affinity.png" />

Ultimately, I decided to make an Apple Watch app for poker players. This was for a few reasons. It’s definitely a niche audience. Poker players who are trying to win often to refer to preflop charts, but pulling out your phone is annoying, so in that sense it solves a problem. While I’m mostly focused on indie hacking, I’m still playing a little poker as a (highly volatile) side income stream, so of course I have a high affinity for professional and semi-professional poker players. Professional poker players are also “prosumers” in that, in some ways they are consumers/individuals, but in some ways they are businesses. If you can help them win more money, like a business, your app has an ROI that justifies spending money on it.

While there’s a lot of chatter about b2b vs b2c, I’m most excited about “b2p” (business 2 prosumer) opportunities since they have the revenue opportunities of b2b but the niche markets reachable with consumer marketing like b2c. I'm not exactly an expert on enterprise sales, so I'm hoping prosumers help me avoid it.

The landing page for my app is here : [https://aceupmysleeve.app](https://aceupmysleeve.app) . 

There’s some controversy around the use of preflop apps at poker that I address on my landing page. Ultimately, my viewpoint is it’s not cheating if you comply with all rules.

One last reason I picked this app is because I do think watchOS apps are overlooked, and I really want to make a first-class watchOS experience for my goal tracker app [Navigoals](https://billprin.com/2022/10/14/why-im-building-navi.html). So I wanted to start with a simple one . This fit the bill, especially because I had to learn a lot about APIs such as WatchConnectivity to even get the IAP working reliably.

### How Long the App Took To Develop

I started the app on November 8, so well into the month, so I technically built it in under a month.

When I started, I was considering options like CoreData vs JSON serialization to store the chart data. Ultimately, I again focused on simplicity and simply hard-coded the charts based on data I found from a reliable source of poker simulations.

Here’s a screenshot from my goal tracker app [Navigoals](https://navigoals.com) that demonstrates when I did Pomodoro tomatoes on this app:


<img height="600" width="600" src=
"{{ site.url }}/assets/sleeve_timestamps.png" />


Note that “SleeveCoding” is timestamps for when I finished an iOS pomodoro tomato. “Sleeve” is general purpose - mostly, I meant to track SleeveCoding and hit Sleeve by accident (still polishing the Navigoals UX ) . SleeveWeb was work on the landing page.

And here’s the calendar view from Navigoals:


<img height="600" width="600" src=
"{{ site.url }}/assets/sleeve_calendar.png" />

The Navigoals UI clearly needs a ton of visual and UX work! Consider my sharing of screenshots here an exercise in #buildinpublic :) 

As you can see, in November I spent around 24 hours on the app. That’s only time I tracked with focused 25 minute Pomodoro tomatoes. If I just chip away at a small issue for ten minutes, I often don’t track it, so this somewhat underestimates my time.

The majority of the time was spent on the iOS app. I also spent 3 hours on the landing page, and 2 hours on the marketing work, such as creating the demo video and posting to Reddit.

You might be surprised that there’s a big fat gap in my work on the app, at one point for 4 days. That was mostly due to an App Store review. From November 20-November 23, I was waiting for Apple to approve my app after they initially rejected it for “illegal gambling.”

### How The Marketing Went

Overall, the app was controversial. Many of the Reddit comments were negative, and many accused me of making an app for “cheating.” 


<img height="100" width="400" src=
"{{ site.url }}/assets/reddit_comments.png" />


<img height="300" width="600" src=
"{{ site.url }}/assets/watches_banned.png" />

Though there was some interesting back-and-forth because many people pointed out that high-profile famous poker players openly admit to using preflop charts. 


<img height="600" width="600" src=
"{{ site.url }}/assets/preflop_discussion.png" />


Overall, I expected some controversy and some negativity. This app mainly was an experiment to make money and learn more about making watchOS apps. If it fails, it’s not too big a deal.

However, I did get a few sales. That will motivate me to keep chipping away at improving it since I still have many ideas to improve both the product and the marketing. I want to move to a subscription model so there can be some recurring revenue, so if you happen to be intersted in the app, get the lifetime purchase while you still can.

### Other Lessons Learned

There were some other important lessons learned. 

One huge mistake I made was not attaching a logo/watermark to my video demo. If you search for "Apple Watch poker", my Reddit post comes up, but my brand is nowhere on it.

While I’m excited about the unexplored potential in watchOS apps, I’ve been frustrated by reviewers who reject me because they don’t understand my app. For example, I’ve been rejected multiple times because they didn’t find IAP content on the iOS, rather than the reviewer taking the time to understand it’s a watchOS app with an iOS control interface.

*edit: hooray! Apple gave me a phone call and told me they would try to work with me more effectively on app reviews, and left a phone contact number to call. Thanks Apple!*

Secondly, there were a lot of complaints about the $20 price point. I think it’s a pretty fair deal given that it helps people at real-money poker; the iPhone costs $600+, and the Apple Watch $400+, so clearly, the target audience has money. However, people are anchored to low price point in app pricing expectations. I do take that feedback with a little grain-of-salt, both because consumers always complain about price, and because my target audience "gets" that my app has a financial ROI. But still, if anything I felt I underpriced my product so I was a little annoyed that I got so much pricing pushback.

I also experimented with ChakraUI for my landing page. One advantage of "smallbets", meaning working on lots of different tiny projects, is that you get more practice at skills relevant to any type of product, such as building effective landing pages, and get the opportunity to try different tools that you might want to adopt.

### Conclusion

$40 is only $40. It’s not exactly going to pay my mortgage.

Still, it’s an exciting start. It shows I validated that at least some people are willing to pay for an app in this space. It allows me to run ads and try to make advertisements profitable rather than light money on fire to acquire non-paying users. If I can use the validation here as a starting point to improve the product and earn a bit more money, it could help extend my entrepreneurial runway while I work on other projects.

Overall, if you’re looking to “go indie” as a developer, I highly recommend going through this exercise at least once. Instead of looking to build the next billion-user app, the next billion-dollar business, the coolest app you can think of, or the most fun app you can think of, instead, filter your extensive list of ideas down to a single criterion - the simplest app that makes money.