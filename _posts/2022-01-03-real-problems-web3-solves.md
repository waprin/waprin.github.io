---
layout: post
title: Real Problems That Web3 Solves, Part 1
description: ""
categories: crypto
tags: [skip, web3, crypto, ethereum]
---

<img src="{{ site.url }}/assets/images/web3_auth.jpeg" />

Web3 is a polarizing topic these days. Many skeptics claim that blockchain does not solve any real problems, and that Web3 is merely a rebranding of cryptocurrency that is only being promoted to increase the market values of those cryptocurrencies. One common refrain is that "blockchain is a solution in search of a problem."

I believe skepticism is an important part of the conversation. I also believe that blockchain and Web3 do solve real problems that previously went unsolved. In this series of posts, I aim to articulate what those problems are and explain how Web3 and blockchain offer novel technology that solves those problems better than previous technological options.

There are a huge amount of investors and influencers promoting the Web3 narrative, and they often make unsubstantiated or hand-wavy claims about the impact that Web3 can have. For example, I often see people claiming that blockchain or Ethereum could somehow address Apple App Store fees, even though I can't find any connection between blockchain and addressing how Apple locks down its hardware devices and takes cuts of apps deployed on them. So there's admittedly a lot of fluff out there and I hope to keep my writing on the topic more grounded in reality. 

If someone in 2007 said, "iPhones are going to be a big part of the future of technology, because they will soon be able to teleport you to the other side of the world", that person would be a fool, but you'd be equally foolish to assume that just because the second half of that statement is untrue, it means the first half is untrue. Similarly, grandiose and inaccurate claims about the potential of blockchain technology do not invalidate legitimate usages of it.

My goal for each problem is:

1. Clearly describe what the problem is and why it matters
1. Clearly describe what non-Web3 solutions already exist and in what ways they're deficient
1. Clearly describe how Web3 and blockchain solutions address the problem in better ways than existing options

## What is Web3 ? Is It Just A Rebrand of Cryptocurrency?

Web3 has been used by a few communities to push future visions of the web, including the "semantic web" where web data is better structured with meaning than currently exists, and "the internet of things" where various devices other than traditional servers and personal computers more natively integrate over the internet. 

Today, the most popular meaning of Web3 relates to the vision of a decentralized web that's been promoted by distributed systems engineers and since co-opted by the broader blockchain community, notably the venture capital firm Andreesen Horowitz. 

One key engineer who has been an advocate for Web3 is Juan Benet who created IPFS, which is a decentralized file hosting solution, similar to Amazon Web Services S3 but without Amazon as a central authority. [Here's a talk from him from 2018 advocating for his vision](https://www.youtube.com/watch?v=l44z35vabvA). 

The [Web3 foundation](https://web3.foundation/about/) was founded by [Dr. Gavin Wood](https://en.wikipedia.org/wiki/Gavin_Wood), a computer scientist notable for designing the Ethereum Rust client, the Ethereum smart contract language Solidity, and the Polkadot cryptocurrency invented to improve the scalability of blockchains by offering cross-chain compatibility solutions.  The foundation describes their mission as "to nurture cutting-edge applications for decentralized software protocols."

So what exactly is the difference between Web3, blockchain, and cryptocurrency? You can think of blockchain and cryptocurrency as technological implementation details, and Web3 as the communities, businesses, and social relationships that form on top of that technology. A similar analogy would be the original World Wide Web, which could have been construed as a rebrand of the underlying technologies of HTML over HTTP over TCP/IP. Those protocols have served as the foundation for virtually all web content for the last 30 years, but it'd certainly be unfair to describe "the Web" as merely a rebranding of HTML/HTTP/TCP/IP since what happens on top of those protocols is much bigger than just the protocols themselves.

Similarly, while it's true that blockchain and cryptocurrency form a large part of the underlying Web3 technology, what's happening on top of those implementation details is much bigger than just those protocols and currencies themselves.

## Problem #1: Owning Your Own Digital Identity & Fixing Authentication

### Describe the Problem

We need some way of saying "who we are" on the internet in a consistent manner. That way we can communicate with others in a verified way and associate with digital data that we own. We also often need that data to be interoperable between different web properties.

### Describe the Existing Solutions

The most common original solution for identity on the web was creating combinations of username and passwords. 

The weaknesses of username and passwords is that it's tedious to create them on many different sites and they are not very interoperable between sites without compromising security.

To solve the interoperability of data, the suite of OAuth protocols (namely OAuth2) was created, which makes it more straightforward for one web app to get scoped permissions to access the data of the user on another webapp.

OAuth2 is mostly a great thing (you can find plenty of criticism about a lot of the details, but the high level idea mostly works). However, it's gotten repurposed to not just be for data interoperability but for identity in general.  People "login" across the web using their Google OAuth or Facebook OAuth login.

The problem we've created is that we've handed ownership of our digital identity - which gets more important with each passing year - to a private company to whom we're not especially important and who owes us nothing in particular. Sure, many mostly trust Google, but there's many good reasons not to trust it, and on principle, it's wrong if we build a world where Sundar Pichai or whoever is leading Google that day has the arbitrary power to delete your identity from the broader internet. 

Many people, including myself, believe that the individual should be able to own their own identity. 

### Describe How Web3 Fixes This

Web3 introduces wallets that use public key cryptography to let people identify via a private key owned by themselves instead of a [OAuth2 login](https://oauth.net/2/) provided by a corporation. It also introduces authentication via a smart contract that enables advances features like social recovery, which lets you recover your account if you lose
your key via a smart contract that takes votes from guardians (friends or paid services).

Many people object to the idea that blockchain is the solution here. The first objection will be that public key cryptography has existed for decades and blockchain does not introduce anything new. The other objection is that the UX is not ready because if someone loses their private key they will lose access to their identity and we need centralized authorities to offer services such as password reset. 

It is true that public key cryptography has existed for a long time. Sysadmins often use private keys to quickly login to their servers and manage who has access to what. It works great. So why have we failed to see this adopted by the broader public? The simple answer is that the UX has been really bad. Regular users are not going to fiddle around with a CLI or key management.

[MetaMask](https://metamask.io/) has implemented private key login via a Chrome extension and [now has 21 million users](https://decrypt.co/86263/ethereum-wallet-metamask-reports-21-million-users). In theory, something like this could have existed a long time ago. In practice, the existence of blockchains and the need for better UX for cryptocurrency incentivized much more investmenets in these tools. 

Money can be a touchy topic in society, but money is an extremely powerful incentive. When most of the money being made on the internet was heading towards big tech companies, it's not surprising that the investments around authentication went into technologies that big tech companies cared about like OAuth2 that would give them greater control and power.

Now cryptocurrency has created a new set of incentives around decentralized technology, so we are seeing better software for decentralized use cases. OAuth2 should be used for what it was intended to, which is for a web service to provide another web service with a user's data given that user's consent. It should not be used as a global digital identifier because that's too important to be owned by anyone but the individual themselves.

## But what if someone loses their private key?

The next major problem you'll hear about is - what if someone loses their private key? They will lose access to that digital identity. Centralized services have methods to verify someone is who they say they are and reset the account.

What blockchain now introduces that solves this "lost keys" problem is called Social Recovery Wallets, which are powered by smart contracts.

Vitalik Buterin, one of the co-founders of Ethereum and one of it's most influential advocates has been pushing for more adoption of social recovery wallets for a long time, but still not enough people know it means. He explains this really well in his blog post on the topic which is an absolute must-read for anyone in the space, as wallet security is super important and social recovery wallets introduce a decentralized way of doing so.

Go ahead and read his post, [Why we need wide adoption of social recovery wallets
](https://vitalik.ca/general/2021/01/11/recovery.html).

Some of you might already be familiar with multisig, which is a similar concept. With multisig, instead of having a single private key, you can have many private keys (say 6), and recover the identity if some number sign off (say 4). 

The idea here is that you could give keys to your friends and family, or to some sort of business service, then if you lose your key, use your friends to "vouch" for you and move the account to a new key.

The problem with multisig is that it pushes a lot of the UX complexity down to the user who's forced to setup all these private keys and manage them. With social recovery wallets, similar multisig logic is moved to smart contracts on the blockchain. This lets recovery be more dynamic, where someone can have one simple wallet with a simple interface that lets them have full control over their funds. But they can dynamically assign friends and family as "guardians" who can vote to reset the account to a new
key.

With social recovery, instead of having to trust Google, you can choose who you trust, and instead trust a given set of friends, family, and services. If you ever lose access to your private key, there is a smart contract encoded on the blockchain that says that if some number of your guardians all agree (you pick the number) then you can move your account to a new private key. You can also do this to require approval from your friends before a certain amount of money moves out of your account, making theft significantly harder.

Vitalik's expresses the importance of this better than I do in his post:

> To me, the goal of crypto was never to remove the need for all trust. Rather, the goal of  crypto is to give people access to cryptographic and economic building blocks that give people more choice in whom to trust, and furthermore allow people to build more constrained forms of trust: giving someone the power to do some things on your behalf without giving them the power to do everything

I agree with Vitalik that as the importance of our digital identity rises, we should control that identity, own it, and get to pick who we choose to help us recover that identity if it's ever compromised.

Social recovery wallets are based on smart contracts which are fundamentally based on the blockchain, and solve a huge problem relating to digital identity ownership that hasn't been solved previously with non-blockchain solutions.

This was the first problem that I wanted to write about. Stay tuned for more posts where I walk through some other problems that blockchain solves best.

I submitted this post to Hacker News, where it generated over 300 thoughtful comments, you can read those comments with [this link](https://news.ycombinator.com/item?id=29797310).
