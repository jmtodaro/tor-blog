---
layout: post
title: "Tor Weekly News — March 4th, 2015"
permalink: tor-weekly-news-—-march-4th-2015
date: 2015-03-04 07:00:00
author: karsten
category: blog
comments: disabled
tags: ["tor weekly news"]
---

Welcome to the ninth issue in 2015 of Tor Weekly News, the weekly newsletter that covers what’s happening in the Tor community.

Tor Browser 4.0.4 and 4.5-alpha-4 are out
=========================================

The Tor Browser team announced new releases in the stable and alpha branches of the privacy-preserving browser. [Version 4.0.4](https://blog.torproject.org/blog/tor-browser-404-released) contains updates to the bundled versions of Firefox, OpenSSL, HTTPS-Everywhere and NoScript (disabling the new NoScript option to make temporary permissions permanent); it also prevents meek from issuing a second update notification.

Meanwhile, following on from the [recent Tor UX sprint](https://blog.torproject.org/blog/ux-sprint-2015-wrapup), [version 4.5-alpha-4](https://blog.torproject.org/blog/tor-browser-45a4-released) incorporates many interface improvements designed to make life easier for Tor users. The connection configuration wizard has been reordered to avoid confusion between network proxies and bridge relays, while a reorganized Torbutton menu now offers a “New circuit for this site” option that removes the need for the user to close all open pages in order to change circuits for one destination. If users do decide to use the “New identity” option, they will now be warned that this involves losing currently-open tabs and windows.

Please see the announcements for full details of the changes, as well as instructions for download and verification.

Reddit donates $82,765.95 to The Tor Project, Inc.
===================================================

One year ago, the [online community Reddit announced](http://www.redditblog.com/2014/02/decimating-our-ads-revenue.html) that it would be donating 10% of its advertising revenue in 2014 to ten non-profits, to be selected by the Reddit community. Voting took place over the last week, and The Tor Project, Inc. placed tenth in the [final ranking](http://www.redditblog.com/2015/02/announcing-winners-of-reddit-donate.html), in good company with other charities like the Electronic Frontier Foundation, Wikimedia Foundation, and the Free Software Foundation, each of which being eligible for a $82,765.95 donation.

Community donations like this are a big step on the way to solving the problem of overreliance on single funding streams — often from national governments — that affects open-source security projects, as [recently discussed by Jillian York](http://jilliancyork.com/2015/02/06/there-are-other-funding-options-than-the-usg/) of the Electronic Frontier Foundation (who came [first](https://twitter.com/reddit/status/571011860260098048) in Reddit’s donation drive). Many thanks to Reddit (the company) and Reddit (the community) for their magnificent gesture of support for privacy and anonymity online — and if you’d like to join them, please take a look at the [Tor Project website](https://www.torproject.org/donate/donate) for ways to contribute!

2015 Winter Tor meeting
=======================

A group of around 70 dedicated Tor contributors is [meeting this week in Valencia](https://trac.torproject.org/projects/tor/wiki/org/meetings/2015WinterDevMeeting), Spain to discuss plans, milestones, deadlines, and other important matters.

This meeting is kindly hosted together with the [OpenITP circumvention tech festival](https://openitp.org/festival/circumvention-tech-festival.html) with public outreach and community events joined or co-hosted by Tor members.

[Notes](https://trac.torproject.org/projects/tor/wiki/org/meetings/2015WinterDevMeeting/Notes) are available from the sessions happening on Monday and Tuesday for those who couldn’t make it this time.

Monthly status reports for February 2015
========================================

The wave of regular monthly reports from Tor project members for the month of February has begun. [Juha Nurmi](https://lists.torproject.org/pipermail/tor-reports/2015-February/000763.html) released his report first, followed by reports from [Nick Mathewson](https://lists.torproject.org/pipermail/tor-reports/2015-February/000764.html), [Philipp Winter](https://lists.torproject.org/pipermail/tor-reports/2015-February/000765.html), [Georg Koppen](https://lists.torproject.org/pipermail/tor-reports/2015-February/000766.html), [Sherief Alaa](https://lists.torproject.org/pipermail/tor-reports/2015-March/000768.html), [Pearl Crescent](https://lists.torproject.org/pipermail/tor-reports/2015-March/000769.html), and [Damian Johnson](https://lists.torproject.org/pipermail/tor-reports/2015-March/000770.html).

Mike Perry reported on behalf of the [Tor Browser team](https://lists.torproject.org/pipermail/tor-reports/2015-March/000767.html).

Miscellaneous news
==================

George Kadianakis [reports preliminary results](https://blog.torproject.org/blog/some-statistics-about-onions) from "a project to study and quantify hidden services traffic." George emphasizes that they "are collecting data from just a few volunteer relays" and that "extrapolating from such a small sample is difficult." Taken with a grain of salt, they "estimate that about 30,000 hidden services announce themselves to the Tor network every day, using about 5 terabytes of data daily." They "also found that hidden service traffic is about 3.4% of total Tor traffic." George, together with Karsten Loesing, wrote a short [technical report](https://research.torproject.org/techreports/extrapolating-hidserv-stats-2015-01-31.pdf) with more details on their results and methods.

Nick Mathewson [announces](https://lists.torproject.org/pipermail/tor-dev/2015-February/008328.html) an important step in stabilizing the Tor 0.2.6.x release series: all work on that series will proceed on the “maint-0.2.6” branch, while work on the next release series 0.2.7.x will happen on the “master” branch. This step allows developers to focus on one branch for fixing bugs and another branch for developing new features.

* * * * *

This issue of Tor Weekly News has been assembled by Harmony, Karsten Loesing, and qbi.

Want to continue reading TWN? Please help us create this newsletter. We still need more volunteers to watch the Tor community and report important news. Please see the [project page](https://trac.torproject.org/projects/tor/wiki/TorWeeklyNews), write down your name and subscribe to the [team mailing list](https://lists.torproject.org/cgi-bin/mailman/listinfo/news-team) if you want to get involved!
