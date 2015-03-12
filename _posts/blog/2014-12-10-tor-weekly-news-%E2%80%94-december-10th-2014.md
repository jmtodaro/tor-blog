---
layout: post
title: "Tor Weekly News — December 10th, 2014"
permalink: tor-weekly-news-—-december-10th-2014
date: 2014-12-10 07:00:00
author: harmony
category: blog
comments: disabled
tags: ["tor weekly news"]
---

Welcome to the forty-ninth issue in 2014 of Tor Weekly News, the [weekly newsletter](https://lists.torproject.org/cgi-bin/mailman/listinfo/tor-news) that covers what’s happening in the Tor community.

Tor Browser 4.0.2 and 4.5-alpha-2 are out
=========================================

Georg Koppen announced new stable and alpha releases by the Tor Browser team. [Tor Browser 4.0.2](https://blog.torproject.org/blog/tor-browser-402-released) fixes the Windows compiler bugs that were resulting in frequent crashes, ensures entries in the cache are once again isolated by URL bar domain, and prevents the user’s locale setting from being leaked by the JavaScript engine. [Tor Browser 4.5-alpha-2](https://blog.torproject.org/blog/tor-browser-45-alpha-2-released) brings further improvements to Torbutton’s new circuit visualization panel, which can now be turned off by visiting about:config and setting “extensions.torbutton.display\_circuit” to “false”, as well as to the security slider.

Both releases contain important security updates and all users should upgrade as soon as possible; please see Georg’s post for full details. You can obtain your copy from the [project page](https://www.torproject.org/projects/torbrowser.html), or through the in-browser updater.

Tails 1.2.1 is out
==================

The Tails team [announced](https://tails.boum.org/news/version_1.2.1/) a new version of the amnesic live operating system. Alongside updates to Linux and Tor Browser, Tails 1.2.1 finally disables the Truecrypt encryption manager, which was abandoned by its developers earlier this year. There have been warnings about this change for several months, but users who have not yet migrated their data away from Truecrypt (or who are not able to) can still access these volumes with cryptsetup by following [Tails’ own guide](https://tails.boum.org/doc/encryption_and_privacy/truecrypt/).

The default configuration of GnuPG has also been changed in line with [accepted best practices](https://help.riseup.net/en/security/message-security/openpgp/best-practices). If you want to take advantage of this, there is a simple step you need to perform; please see the team’s post for more details, and get your copy of the new Tails from the [download page](https://tails.boum.org/download/) or through the incremental updater.

More monthly status reports for November 2014
=============================================

The wave of regular monthly reports from Tor project members for the month of November continued, with reports from [Pearl Crescent](https://lists.torproject.org/pipermail/tor-reports/2014-December/000718.html), [Sukhbir Singh](https://lists.torproject.org/pipermail/tor-reports/2014-December/000719.html), [Leiah Jansen](https://lists.torproject.org/pipermail/tor-reports/2014-December/000720.html), [Matt Pagan](https://lists.torproject.org/pipermail/tor-reports/2014-December/000721.html), [Arlo Breault](https://lists.torproject.org/pipermail/tor-reports/2014-December/000723.html), [Colin C.](https://lists.torproject.org/pipermail/tor-reports/2014-December/000724.html), and [Nicolas Vigier](https://lists.torproject.org/pipermail/tor-reports/2014-December/000725.html).

Karsten Loesing reported on behalf of the [Tor Network Tools team](https://lists.torproject.org/pipermail/tor-reports/2014-December/000722.html), and Roger Dingledine sent out the report for [SponsorF](https://lists.torproject.org/pipermail/tor-reports/2014-December/000726.html).

Miscellaneous news
==================

George Kadianakis [sent out](https://lists.torproject.org/pipermail/tor-dev/2014-December/007928.html) an updated draft of the proposal to safely collect hidden service statistics from Tor relays.

Nick Mathewson gave a [talk](https://www.youtube.com/watch?v=rIf_VZQr-dw) to the Computer Systems Security class at MIT on the subject of “Anonymous Communication”.

David Fifield [summarized](https://lists.torproject.org/pipermail/tor-dev/2014-December/007916.html) the costs incurred in November by the infrastructure for the meek pluggable transport.

The Tails team [wondered](https://mailman.boum.org/pipermail/tails-dev/2014-December/007580.html) about the best way to prioritize adding support for pluggable transports: “Assuming we add support for Scramblesuit in Tails 1.3, then what usecases won’t we be supporting, that we could support better with obfs4 or meek?”

usprey wrote up a [guide](https://lists.torproject.org/pipermail/tor-relays/2014-December/005907.html) to configuring a Tor relay on a server running Arch Linux: “All and any feedback will be appreciated! Are there any privacy concerns about using pdnsd to cache DNS locally?”

Jacob Appelbaum [recommended](https://mailman.boum.org/pipermail/tails-dev/2014-December/007537.html) possible ways to reduce the attack surface presented by the kernel and the firewall in Tails. He also [compiled](https://mailman.boum.org/pipermail/tails-dev/2014-December/007588.html) a dataset containing historical hashes and signatures of Tails files: “In the future, I’ll write a program that uses the dataset in a useful manner. In an ideal world, we’d have a way to use a Tails disk to verify any other Tails disk.”

Tor help desk roundup
=====================

Users often write to find out how they can help the Tor Project. There are several ways to help out.

If you have access to a server, consider setting up a [Tor relay](https://www.torproject.org/docs/debian) to expand the network, or a [bridge relay](https://trac.torproject.org/projects/tor/wiki/doc/PluggableTransports#Howtosetupabridgewithpluggabletransports) to help internet users stuck behind censorship.

If you’re a coder, see if any of the projects on our [volunteer page](https://www.torproject.org/getinvolved/volunteer#Projects) capture your interest. You can also look for tickets on our [bug tracker](https://trac.torproject.org/projects/tor/report) that are filed with the “easy” component if you want to submit some patches.

If you’re interested in doing outreach, consider joining the [Tor Weekly News team](https://trac.torproject.org/projects/tor/wiki/TorWeeklyNews).

If you’d like to get involved with translations, please join a team on our [Transifex](https://www.transifex.com/projects/p/torproject/). If a team for the language you’d like to translate into does not yet exist (check carefully), please go ahead and request a new team. It will take a day or two for the team to be approved, so please be patient.

News from Tor StackExchange
===========================

strand raised a question about the code regarding [rendezvous and introduction points](https://tor.stackexchange.com/q/848/88). Within src/or/rendservice.c there are several occurrences of onion\_address, and strand wants to know which function catches what from a hidden service. If you can answer this question, please come to Tor’s Q&A page and give us some insights.

This week in Tor history
========================

[A year ago this week](https://lists.torproject.org/pipermail/tor-news/2013-December/000024.html), the Freedom of the Press Foundation launched its “Encryption Tools for Journalists” [crowdfunding campaign](https://freedom.press/bundle/encryption-tools-journalists), distributing the proceeds to five free software security projects, including the Tor Project and Tails. As of this writing, 1256 donors have contributed $136,977.05 in support of journalists’ right to communicate with sources and carry out research without being subjected to invasive surveillance. Thanks to the FPF and to everyone who has donated so far!

* * * * *

This issue of Tor Weekly News has been assembled by Matt Pagan, qbi, David Fifield, Arlo Breault, Karsten Loesing, and Harmony.

Want to continue reading TWN? Please help us create this newsletter. We still need more volunteers to watch the Tor community and report important news. Please see the [project page](https://trac.torproject.org/projects/tor/wiki/TorWeeklyNews), write down your name and subscribe to the [team mailing list](https://lists.torproject.org/cgi-bin/mailman/listinfo/news-team) if you want to get involved!
