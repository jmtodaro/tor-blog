---
layout: post
title: "Some statistics about onions"
permalink: some-statistics-about-onions
date: 2015-02-26 16:00:57
author: asn
category: blog
comments: open
tags: ["hidden services", "onions", "statistics"]
---

**Non-technical abstract:**

  
 We are starting a project to study and quantify hidden services traffic. As part of this project, we are collecting data from just a few volunteer relays which only allow us to see a small portion of hidden service activity (between 2% and 5%). Extrapolating from such a small sample is difficult, and our data are preliminary.

We've been working on methods to improve our calculations, but with our current methodology, we estimate that about 30,000 hidden services announce themselves to the Tor network every day, using about 5 terabytes of data daily. We also found that hidden service traffic is about 3.4% of total Tor traffic, which means that, at least according to our early calculations, 96.6% of Tor traffic is \*not\* hidden services. We invite people to join us in working to research methodologies and develop systems for better understanding Tor hidden services.  

* * * * *

  

Hello,

Over the past months we've been working on hidden service statistics. Our goal has been to answer the following questions:

-   **"Approximately how many hidden services are there?"**
-   **"Approximately how much traffic of the Tor network is going to hidden services?"**

  

We chose the above two questions because even though we want to understand hidden services, we really don't want to harm the privacy of Tor users. From a privacy perspective, the above two questions are relatively easy questions to answer because we don't need data from clients or the hidden services themselves; we just need data from hidden service directories and rendezvous points. Furthermore, the measurements reported by each relay cannot be linked back to specific hidden services or their clients.

Our first move was to [research various ways we could collect these statistics in a privacy-preserving manner](https://lists.torproject.org/pipermail/tor-dev/2014-November/007816.html). After [days of discussions on obfuscating statistics](https://lists.torproject.org/pipermail/tor-dev/2014-December/007911.html), we began writing [a Tor proposal](https://gitweb.torproject.org//torspec.git/tree/proposals/238-hs-relay-stats.txt) with our design, as well as [code that implements the proposal](https://bugs.torproject.org/13192). The code has since been reviewed and [merged to Tor](https://blog.torproject.org/blog/tor-0262-alpha-released)! The statistics are currently disabled by default so [we asked volunteer relay operators to explicitly turn them on](https://lists.torproject.org/pipermail/tor-relays/2014-December/005953.html). Currently there are about 70 relays publishing measurements to us every 24 hours:  
   
  
 ![Number of relays reporting stats](https://people.torproject.org/~asn/hsstsblgpst/num-reported-stats.png)  
   
  
 So as of now we've been receiving these measurements for over a month, and we have thought a lot about how to best use the reported measurements to derive interesting results. We finally have some *preliminary results* we would like to share with you:

How many hidden services are there?
-----------------------------------

All in all, it seems that every day about 30000 hidden services announce themselves to the hidden service directories. Graphically:  
   
  
 ![Number of hidden services](https://people.torproject.org/~asn/hsstsblgpst/extrapolated-onions.png)  
   
  
 By *counting the number of unique hidden service addresses seen by HSDirs*, we can get the approximate number of hidden services. Keep in mind that we can only see between 2% and 5% of the total HSDir space, so the extrapolation is, naturally, messy.

How much traffic do hidden services cause?
------------------------------------------

Our preliminary results show that hidden services cause somewhere *between 400 to 600 Mbit of traffic per second*, or equivalently about *4.9 terabytes a day*. Here is a graph:  
   
  
 ![Hidden services traffic volume](https://people.torproject.org/~asn/hsstsblgpst/extrapolated-cells.png)  
   
  
 We learned this by getting rendezvous points to publish the total number of cells transferred over rendezvous circuits, which allows us to learn the approximate volume of hidden service traffic. Notice that our coverage here is not very good either, with a probability of about 5% that a hidden service circuit will use a relay that reports these statistics as a rendezvous point.

A related statistic here is *"How much of the Tor network is actually hidden service usage?"*. There are [two different ways](https://lists.torproject.org/pipermail/tor-dev/2015-February/008249.html) to answer this question, depending on whether we want to understand what clients are doing or what the network is doing. The fraction of hidden-service traffic at Tor clients differs from the fraction at Tor relays because connections to hidden services use 6-hop circuits while connections to the regular Internet use 3-hop circuits. As a result, the fraction of hidden-service traffic entering or leaving Tor is about half of the fraction of hidden-service traffic inside of Tor. Our conclusion is that about *3.4% of client traffic is hidden-service traffic, and 6.1% of traffic seen at a relay is hidden-service traffic*.

Conclusion and future work
==========================

In this blog post we presented some preliminary results that could be extracted from these new hidden service statistics. We hope that this data can help us better gauge the future development and maturity of the *onion space* as well as detect potential incidents and bugs on the network. To better present our results and methods, [we wrote a short technical report](https://research.torproject.org/techreports/extrapolating-hidserv-stats-2015-01-31.pdf) that outlines the exact process we followed. We invite you to read it if you are curious about the methodology or the results.

Finally, this project is only a few months old, and there are various plans for the future. For example:

-   There are more interesting questions that we could examine in this area. For example: "How many people are using hidden services every day?" and "How many times does someone try to visit a hidden service that does not exist anymore?."

    Unfortunately, some of these questions are not easy to answer with the current statistics reporting infrastructure, mainly because collecting them in this way could reveal information about specific hidden services but also because the results of the current system contain too much obfuscating data (each reporting relay randomizes its numbers a little bit before publishing them, so we can learn about totals but not about specific events).

    For this reason, [we've been analyzing various statistics aggregation protocols](https://lists.torproject.org/pipermail/tor-dev/2015-January/008086.html) that could be used in place of the current system, allowing us to safely collect other kinds of statistics.

-   We need to incorporate these statistics in [our Metrics portal](https://metrics.torproject.org/) so that they are updated regularly and so that everyone can follow them.
-   Currently, these hidden service statistics are not collected in relays by default. Unfortunately, that gives us very small coverage of the network, which in turn makes our extrapolations very [noisy](https://en.wikipedia.org/wiki/Noise_%28signal_processing%29). The main reason that these statistics are disabled by default is that similar statistics are also disabled (e.g. CellStatistics). Also, this allows us more time to consider privacy consequences. As we analyze more of these statistics and think more about statistics privacy, we should decide whether to turn these statistics on by default.

    It's worth repeating that the current results are preliminary and should be digested with a grain of salt. We invite statistically-inclined people to review our code, methods, and results. If you are a researcher interested in digging into the measurements themselves, you can find them in the [extra-info descriptors of Tor relays](https://collector.torproject.org/archive/relay-descriptors/extra-infos/).

    Over the next months, we will also be thinking more about these problems to figure out proper ways to analyze and safely measure private ecosystems like the onion space.

  

Till then, take care, and enjoy Tor!
