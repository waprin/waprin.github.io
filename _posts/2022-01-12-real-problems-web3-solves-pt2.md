---
layout: post
title: Real Problems That Web3 Solves, Part 2
description: ""
categories: crypto
tags: [web3, crypto, ethereum]
---

<img src="{{ site.url }}/assets/images/webuywesell.jpeg" height="400"/>


[In Part 1 of this series](https://billprin.com/2022/01/03/real-problems-web3-solves.html), I addressed why web3 is much more than a rebranding of cryptocurrency. I wrote about how web3 has onboarded tens of millions on users onto decentralized auth, a problems that preeminent web companies like Mozilla attempted to solve with products like Persona, and shut down due to lack of traction. 

I also wrote about how blockchains solve one of the key UX issues of decentralized authentication - loss of private key - via social recovery wallets on smart contracts, novel technology unique to blockchains.


The post generated over 300 comments with a lot of thoughtful discussion on Hacker News, [which you can read here](https://news.ycombinator.com/item?id=29797310).


To reiterate my goal for each problem in this series, after some introductory text providing some context, I aim to:

1. Clearly describe what the problem is and why it matters
1. Clearly describe what non-Web3 solutions already exist and in what ways they’re deficient
1. Clearly describe how Web3 and blockchain solutions address the problem in better ways than existing options

This blog post series is semi-technical and some background in software engineering is helpful but not required. If you want an amazing, interactive walkthrough of the elliptic curve mathematics form the foundation of blockchain, I'd highly recommend  Andrej Karpathy's post titled [A from-scratch tour of Bitcoin in Python](http://karpathy.github.io/2021/06/21/blockchain/). Andrej is a leading deep learning researcher and the Director of Artifical Intelligence at Tesla. For now, let's just read the first line:

> I find blockchain fascinating because it extends open source software development to open source + state. 

I think there's a lot more insight in that line than one might pick up on first read, so hold that thought, as it serves as the foundation for the rest of this post.

It's impossible to understand any revolution without understanding the historical context in which it took place. In the case of the blockchain revolution, it has stood on the shoulders of a giant revolution that took place before it and to which it's deeply indebted. This preceding revolution is notable in part because it's leader started it entirely by accident. The leader's name was Linus Torvalds, and his revolution was named Linux.

# Just For Fun

<img src="{{ site.url }}/assets/images/justforfun.jpeg" height="400"/>

In 1991, a 22 year old Finnish student named Linus Torvalds started writing an open source operating system. If at the time, someone asked him what problems his s, he'd probably tell you that it didn't solve any problems. It merely scratched his own itch to build an operating system where all the code was open for everyone.

You could easily find much more functional operating systems such as SunOS developed by Sun Microsystems. Linus set out not to solve a problem, but simply to have fun, as the name of his memoir suggests. He was creating a toy.

Today, that toy operating system is what the vast majority of the  modern web runs on.

Google? Linux. 
Amazon? Linux. 
Wikipedia? Linux. 
Stack Overflow? Windows, but you get the idea, most of the web runs on Linux. 

This was in no way an obvious outcome in the early 90s, because Linux was really not a professional operating system written by real established companies but it was a toy project, for fun, for passionate hobbyists. 

Many people assumed that toy projects were not suitable for real important use cases. As an example,one reason Elon Musk left PayPal was because he thought they should migrate their infrastructure to Windows instead of Linux. I wonder if in 2022, Elon's love of "joke" projects like Dogecoin in any ways relate to the fact that one of his most notable career missteps was underestimating the power of a toy project.

But why did Linux take over the internet? For one thing, sometimes "hobbyists" are actually more skilled than their professional counterparts precisely because the type of person who will work on something for free has more intrinsic motivation to do good work then someone working for money. 

## The Cathedral And The Bazaar

<img src="{{ site.url }}/assets/images/cathedral.jpg" height="400"/>


There's another important dynamic at play besides that though, which Eric S Raymond wrote about in his seminal essay on Free Open Source Software, titled [The Cathedral and The Bazaar](http://www.catb.org/~esr/writings/cathedral-bazaar/cathedral-bazaar/index.html#catbmain), first published in 1997. Here's excerpts from the opening paragraph in which I splice out some notable parts.


>Linux is subversive...Linux overturned much of what I thought I knew.....I believed there was a certain critical complexity above which a more centralized, a priori approach was required... No quiet, reverent cathedral-building here—rather, the Linux community seemed to resemble a great babbling bazaar of differing agendas and approaches out of which a coherent and stable system could seemingly emerge only by a succession of miracles.

Another well-known quote from The Cathedral and The Bazaar was dubbed Linus's Law and is written as follows:

> Given enough eyeballs, all bugs are shallow. I dub this: Linus's Law
My original formulation was that every problem will be transparent to somebody. 

> Linus demurred that the person who understands and fixes the problem is not necessarily or even usually the person who first characterizes it. Somebody finds the problem,'' he says, and somebody else understands it.

The central thesis of Raymond is that the collective wisdom of the crowd along with transparency, led to better systems and better outcomes for all parties. This was the so-called bazaar style of development. But what is a bazaar? It's another word for a _market_.

## Describe the Problem


### Problem #2: We need markets to exchange goods, services, and financial assets

### Problem #2A: We need someone to make a market

The world needs markets to exchange goods, services, and financial assets like stocks, futures, and currencies.

A farmer might want to plant corn now, but sell in a year at a fixed price. Thus, the futures market and the Chicago Mercantile Exchange. An entrepeneur might want to raise money, but investors will be nervous without some liquidity for the shares they buy. Thus, the stock market, and the New York Stock Exchange. 

While at times, the finance industry seems abstract and divorced from the real world, it serves a critical function in society, and every developed country has a functional finance system. Many tall buildings have been built in New York, Chicago, London, and Tokyo because the symbolic pieces of paper and digital account balances do have real world importance.

### Describe the Existing Solutions

Let's return to the image at the top of the blog post. That's probably a familiar site for anyone who's traveled internationally, as it's a currency exchange inside an airport.

<img src="{{ site.url }}/assets/images/webuywesell.jpeg" height="400"/>


It probably doesn't surprise you to see that there is a large difference between what the currency exchange will buy at and sell at. The price that they're willing to buy at is called the "bid", and the price they're willing to sell at is called "the ask". The difference between the bid and the ask is called "the spread", or "the take". 

Most markets operate this way in some capacity or another. In a larger, more liquid market, there might be many people placing bids, and many people placing asks, and occasionally someone "takes" a bid or ask from the market and makes the exchange, setting a new market price.

As you also probably know, at the airport currency exchange the spread is quite large. If you start with $100 US dollars, exchange them for Euros, and then immediately exchange it back for dollars, you will end up with a lot less dollars than you started with because of the spread.

Most people know that the airport is a really bad place to exchange currency if you're looking to get a good rate. But why is that? Is it because people who work in airports are especially greedy? I would argue that the rate is very bad mostly because there is very little competition. Once you are already in the airport, only a few licensed businesses can exchange your currency, so they don't have much direct competition and can charge a very high spread. 

Imagine someone like myself that lives in the United States but has some extended family in Europe. Given that I'm somewhat likely to visit Europe sometime in the next few years, I don't mind having some of my money already in euros so that I can spend it the next time that I visit. If one of my friends wanted to trade dollars for euros, since I hold both, I'd happily offer them a better rate than the airport exchange. But do so, I need some mechanism to easily allow my dollars/euros to be swapped.

Blockchain makes it very easy for anyone to provide liquidity to the market via [yield farming](https://www.coindesk.com/markets/2021/11/03/a-look-into-curves-ecosystem-defis-centerpiece/). The person looking to exchange currency wins because they get a better rate and save money. The person providing liquidity makes passive income for holding two currencies, something they might have wanted to do anyway. The only person who loses out is a middleman who was only able to charge high fees due to lack of competition.

Before exploring that more, first let's look at another dimension of this problem.

### Problem #2B: We need our financial markets to be fair and transparent

It's very important that our financial markets are fair. It's bad if market participants can do things like front-run trades or charge prices higher than what the market naturally converged to.
 
### Describe the Existing Solution

Why do the existing financial markets not have such a great reputation? In large part, because they're unfair. '

<img src="{{ site.url }}/assets/images/darkpools.jpeg" height="400"/>


In 2011, the book Dark Pools: The Rise of A.I. Trading Machines and the Looming Threat to Wall Street was published. I got a free copy and read it because the books writes about a startup called Selerity that I worked at when the book was published. We scraped the web for financial media events, and most of our customers were high-frequency traders, so I got to see some of that industry up close. From far away, our markets look unfair, but you get up close to examine them, they look _extremely_ unfair.

Let me directly quote, an excerpt directly from the book:

> The rep told Bodek about the kind of orders he should use—orders that wouldn’t get abused like the plain vanilla limit orders; orders that seemed to Bodek specifically designed to abuse the limit orders by exploiting complex loopholes in the market’s plumbing. The orders Bodek had been using were child’s play, simple declarative sentences sent to exchanges such as “Buy up to $20.” These new order types were compound sentences, with multiple clauses, virtually Faulknerian in their rambling complexity. The end result, however, was simple: Everyday investors and even sophisticated firms like Trading Machines were buying stocks for a slightly higher price than they should, and selling for a slightly lower price and paying billions in “take” fees along the way.
Patterson, Scott. Dark Pools (p. 49). Crown. Kindle Edition. 

For those who don't know, when you buy or sell an asset on an exchange there's a few ways to make your order. You can set a "limit" order, that might say, "Buy 1 share of Apple for $172". If Apple goes to $173 before the order is filled, your order will just be canceled. You can also set a "market order", that says "Buy 1 share of Apple at whatever the market price is."

What Patteron's book explores is that certain preferred traders were getting special order types _unavailable to anyone else_ that gave them unique advantages not enjoyed by any other market participants. That's obviously grossly unfair, but it's a reality of existing markets that have no transparency.

In 2021, Robinhood halted trading on Gamestop shares, citing liquidity concerns with respect to their brokerage house.  What's especially notable about the event  was that the trading was halted asymmetricaly meaning you could only sell but not buy. That can only make the price go down, never up, benefiting those on the short side of the trade.

Much has been written and agonized over this event, so I'll skip over a lot of the details, but I want to emphasize one aspect of what happened.

Robinhood customers were allowed to sell their Gamestop stock, so there must have been a buyer. That buyer can't have been another retail trader on Robinhood, since they were not allowed to buy. So _someone_, likely not a retail trader, was buying during the trade halting. 

I'd love to dig a little deeper into who that might be, but I have no way of doing so, because there's no transparency to these markets. I'm not suggesting I'd find anything, but there might be some interesting clues.

The SEC plays an important role here, but there is simply too much complex stuff going on to realistically expect the SEC to perfectly regulate everything. That's especially true because the industry the SEC is regulating is filled with many cunning and intelligent people who are much more strongly incentivized to make money through bending/breaking the rules than the SEC is incentivized to stop them. Often times, the fines the SEC levies are not that significant to these billion dollar companies, such as their [fine of Robinhood](https://www.sec.gov/news/press-release/2020-321) for cheating their customers out of fair market prices.

## Describe How Web3 Fixes This

<img src="{{ site.url }}/assets/images/uniswap.png" height="200"/>


In 2017, a  young mechanical engineer named Hayden Adams was laid off from his first job at Siemens. Despite having no coding background, he dove into an area that Vitalik Buterin has been advocating since the inception of Ethereum - decentralized exchanges. He found great success and created one of the canonical web3 applications: [Uniswap](https://uniswap.org/).

Despite being a toy market, by a young, inexperienced engineer, Uniswap already has billions of dollars worth of volume traded every day. It's hard for me to not see the echoes of Linux in this toy market. And just like Linux you can see all the smart contracts and code that [powers Uniswap for free on Github](https://github.com/Uniswap), and contribute your changes to the project yourself. 

Decentralized exchanges solve the same essential problem that humanity has addressed for most of civilization - making markets. They do so in some novel ways. They do have many disadvantages, some of which might improve as the technology progresses. But they also have a lot of distinct advantages.

One interesting advantage is that anyone can provide liquidity to the market. In the aforementioned currency exchange example, you can hold two currencies on the decentralized exchange and without doing anything get a small fee when you let a market participant swap your currencies.  

This is the burgeoning field of Decentralized Finance (DeFi) which is taking on traditional finance (TradFi) head on, and is probably the fastest growing sector of web3.

Some may object to DeFi being web3, since finance seems so distant from the fun world of consumer web we've grown used to. But if anything the divergence of consumer finance from consumer web is a reflection of slow innovation in the TradFi sector. In part of 1 of this series, and I mentioned that OAuth became a standard for data exchange. Despite that, companies like Plaid had to spring up to add OAuth to financial products because the finance companies chose not to do it themselves despite massive demand. 

Because of this, Plaid's whole business model is based on a incredibly broken security model. If you suggested Plaid's security model at a Google or Amazon or Pinterest (shoutout) systems design interview, you'd get walked out the door as a no-hire, becaues it's fundamentally broken .  See the post, [Plaid is still a phishing site](https://thekeesh.com/2020/01/plaid-is-still-a-phishing-site/). I can't let anyone build an app on my Bank Of America account without putting my password at unnecessary risk and exposing _all_ of my financial data instead of selecting the data I am comfortable sharing with app. The whole thing is an abject security disaster, nobody who understands cybersecurity could make a good faith argument otherwise, yet everyone looks past it because there was no other way for our financial data to be "programmable" - for example so someone can make a budgeting app such as Mint. 

But I'll give Plaid credit that they tried to solve a problem that the TradFi sector refused to solve themselves. I also think it's very notable that despite RobinHood being the trading darling of millennials and zoomer generation, they don't have an official API. TradFi is consistently a decade behind consumer web innovation.

TradFi is not interested in keeping up with the technological pace of the web _except_ when it comes to their backend trading systems that professionals make money on. As previously mentioned, TradFi is _very_ advanced if not more advanced than many Silicon Valley tech darlings when it comes to making themselves money with advanced trading systems. They just haven't extended that passion for technology to the software they offer their customers.

Decentralized finance also offers a lot more transparency than we're used to in the TradFi sector (Traditional Finance). It moves at a faster pace because it's open source. For example, if you're curious how [Magic Internet Money](https://abracadabra.money/) (MIM) provides decentralized lending, you can a site like etherscan.deth.net to read their whole underlying smart contract straight from the ethereum blockchain right into your web browser.

Check that out right here: [MIM smart contract code via etherscan.deth.net](https://etherscan.deth.net/address/0x59e9082e068ddb27fc5ef1690f9a9f22b32e573f)

In 2021, there was some controversy when it discovered that an employee of OpenSea, the #1 NFT trading platform, was buying [NFTs that were going to be featured on their front page](https://techcrunch.com/2021/09/15/opensea-admits-incident-as-top-exec-is-accused-of-trading-nfts-on-insider-information/) before they were, then flipping for a higher price. 

While that's absolutely shameful behavior, and many point to as proof of the fraudulent behavior in the crypto world (which there's plenty of), the part of the story that didn't get enough attention is how the employee was caught. 

He was caught because a third-party unaffiliated with OpenSea looked at the transactions on the Ethereum blockchain, noticed the suspicious behavior, and [called it out on Twitter](
https://twitter.com/0xZuwu/status/1437921263394115584). Unlike the Gamestop fiasco, people were able to see what addresses were trading what assets, and from those clues, were able to figure out some sketchy market behavior that might have otherwise gone unnoticed.

## Why We Don't Need Everyone To Run A Server/Node (The Tipping Point)

Some recent criticism of web3 is that not everyone wants to run a server, not everyone wants to run a node, not everyone will validate everything. Notably the Signal founder Moxie [wrote about this in a fantastic piece](https://moxie.org/2022/01/07/web3-first-impressions.html) that deservedly went very viral. There was a ton of important criticism in that blog post, but I will note that I'm less concerned whether everyone runs a node or not. It's not necessarily that critical that everyone does run a node but that everyone _can_ run a node. 


<img src="{{ site.url }}/assets/images/tippingpoint.jpeg" height="400"/>


Malcolm Gladwell wrote about this concept is his best-selling book [The Tipping Point](https://en.wikipedia.org/wiki/The_Tipping_Point) where he talked about _mavens_ or information specialists. These are people, who according to the Wikipedia article on the book:

> Mavens are "information specialists", or "people we rely upon to connect us with new information." They accumulate knowledge, especially about the marketplace, and know how to share it with others. Gladwell cites Mark Alpert as a prototypical Maven who is "almost pathologically helpful", further adding, "he can't help himself." In this vein, Alpert himself concedes, "A Maven is someone who wants to solve other people's problems, generally by solving his own." According to Gladwell, Mavens start "word-of-mouth epidemics" due to their knowledge, social skills, and ability to communicate. As Gladwell states: "Mavens are really information brokers, sharing and trading what they know."

In his book, he talks about how the grocery stories have to be mostly honest about the price of grapes and detergent, even though most people don't know exactly what those prices should be. There will be _mavens_ who understand the markets and will make a big deal if the grocery stores diverge too far from market prices. Similarly, the _mavens_ of the DeFi world can be an invaluable asset in helping understand financial markets and keeping them fair.

We don't need everyone in the world to run an Ethereum node to keep the market honest, we just need some _mavens_ to. Moving more of the financial world into an open-source ecosystem enables those _mavens_ to help us whereas they can not help us if they have no access to the market transactions as is the case in most TradFi markets.

The reason why in 2005 I could get my sound system working on my Linux desktop because someone in Taiwan that I will never meet posted a kernel module to a mailing list is the same reason that blockchain markets will be more fair because they will have more eyes and therefore more bugs (fraud, etc) will be shallow. 

## But isn't it all a navel-gazing, self-referential, zero-utility toy?

The biggest objection you will face to decentralized finance advocacy is that today, for now, there's a lot of "toy" markets. It's blockchain tokens for the other blockchain tokens without a clear tie to the real economy. It can all feel a little made up.

The financial markets have always been about trading symbolic pieces of paper that only loosely connect to the real world, mostly via a shared belief that they do connect. Already, there is a lot of work going on to connect blockchain markets to real markets. For example, Ethereum has the concept of [oracles](https://ethereum.org/en/developers/docs/oracles/) which allow for decentralized agreement on real world events that smart contracts can refer to. As a result, some of the first markets we're seeing our ["synthetic" markets](https://www.gemini.com/cryptopedia/synthetix), which can use oracles to learn the price of real-world assets and create blockchain assets that reflect that price. 

There's also development around the idea of ["algorithmic" stablecoins](https://101blockchains.com/algorithmic-stablecoins/). Stablecoins tie a cryptoasset to a real currency price. Historically this was done via centralized entities, with a lot of doubt around those centralized entities. The future that's developing is yet again an elimination of centralized entities replaced by algorithms that we can better understand, trust, and rely on.

While today's decentralized finance is nascent, immature, and rife with fraud and scams, the pace of innovation is undeniable. The diagram looks something like this:

<img src="{{ site.url }}/assets/images/defi.png" height="400"/>

Just like Linus Torvalds has an eponymous law named after him, there's another eponymous law in programming called Atwood's Law that goes as follow:

> Any application that can be written in JavaScript, will eventually be written in JavaScript.

The reason Jeff Atwood advocated for this law is there a natural tendency for software to end up on platforms that are interoperable and built on open-standards. This tends to lead to more innovation and better integrated consumer experiences. In the future, we might see a similar dynamic develop, such as:

> Any financial market that can operate on blockchain, will eventually operate on blockchain.

It might take a very long time before we see the New York Stock Exchange operate on blockchain, just like we might have to wait a long time until desktop software as amazing as [Ableton Live](https://www.ableton.com/) arrives on the browser. But it might get there, and it might happen sooner than we expect.

Decentralized finance is subversive, and it's going to overturn much of what we thought we knew. It will resemble a great babbling bazaar of differing agenda and approaches. And I believe that the end result will be more transparent markets, more innovative markets, more fair markets, and a coherent stable system that will seemingly emerge only by a succession of miracles. 

Thanks for reading, and stay tuned for my next post in this series on problems that blockchains solves best.
