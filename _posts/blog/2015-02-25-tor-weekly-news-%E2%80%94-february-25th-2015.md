---
layout: post
title: "Tor Weekly News — February 25th, 2015"
permalink: tor-weekly-news-—-february-25th-2015
date: 2015-02-25 07:00:00
author: harmony
category: blog
comments: disabled
tags: ["tor weekly news"]
---

Welcome to the eighth issue in 2015 of Tor Weekly News, the [weekly newsletter](https://lists.torproject.org/cgi-bin/mailman/listinfo/tor-news) that covers what’s happening in the Tor community.

Tor 0.2.6-alpha-3 is out
========================

Nick Mathewson [announced](https://blog.torproject.org/blog/tor-0263-alpha-released) the third (“and hopefully final”) alpha release in the Tor 0.2.6.x series. The major user- and operator-facing changes in this release include support for AF\_UNIX sockets, allowing high-risk applications to reach a local Tor without having to enable other kinds of networking activity; a new warning for relay operators, in order to make it even harder to accidentally run an exit node; improvements and additions to the directory system; and much else besides.

See Nick’s announcement for the full changelog, and download your copy of the source code from the [distribution directory](https://dist.torproject.org/), but note that “this is an alpha release”, so “please expect bugs”.

Tails 1.3 is out
================

The Tails team [announced](https://tails.boum.org/news/version_1.3/) version 1.3 of the anonymous live operating system. This release brings several major new features, including Bitcoin support with Electrum; connections to Tor using the obfs4 pluggable transport; an AppArmor profile to protect the filesystem against some kinds of attack on Tor Browser; a simpler Tails drive creation process on Mac and Linux; and more intuitive handling of computer trackpads.

See the announcement for links to the full list of changes and known issues, and download your copy from the [website](https://tails.boum.org/download/) or, if you already have a running Tails, using the incremental update system.

CITIZENFOUR wins many awards
============================

Laura Poitras’ documentary film [CITIZENFOUR](https://citizenfourfilm.com/), recording the initial encounters between herself, journalist Glenn Greenwald, and the American surveillance whistleblower (and sometime [Tor relay operator](http://www.wired.com/2014/05/snowden-cryptoparty/)) Edward Snowden, has been decorated at numerous awards ceremonies over the [past few months](https://en.wikipedia.org/wiki/Citizenfour#Awards_and_nominations) for its artistic and political achievement.

The filmmakers have been tireless in their activism on behalf of Tor and the free software community both in the mainstream press and at [community conferences](https://media.ccc.de/browse/congress/2014/31c3_-_6258_-_en_-_saal_1_-_201412282030_-_reconstructing_narratives_-_jacob_-_laura_poitras.html); upon [receiving the Ridenhour Documentary Film Prize](http://www.nationinstitute.org/blog/prizes/4376/%22citizenfour%22_will_receive_the_ridenhour_documentary_film_prize/) last week, Laura called attention to the role of these projects in the production process: “This film and our NSA reporting would not have been possible without the work of the Free Software community that builds free tools to communicate privately. The prize money for the award will be given to the Tails Free Software project.”

CITIZENFOUR went on to win the [Independent Spirit](http://www.filmindependent.org/press/press-releases/2015-film-independent-spirit-awards-winners-announced/) and [Academy](http://www.oscars.org/oscars/ceremonies/2015) Awards for Best Documentary Feature over the weekend. The recognition is richly deserved. Thanks to Laura and her colleagues for their extraordinary work over the last two years!

Miscellaneous news
==================

Giovanni Pellerano [released](https://lists.torproject.org/pipermail/tor-talk/2015-February/036969.html) a security advisory for a bug in GlobaLeaks that was introduced on 28th January 2015, and fixed on 16th February. The bug could have allowed an attacker to read any file in the /var/globaleaks/ directory with the exception of the Tor onion service key; if you installed or upgraded your GlobaLeaks instance on or between those dates, please see Giovanni’s announcement for more details, and upgrade again as soon as possible.

Nathan Freitas [announced](https://lists.mayfirst.org/pipermail/guardian-dev/2015-February/004261.html) Orbot version 15-alpha-4, featuring bridge scanning and distribution via QR code, and simpler configuration for pluggable transports like meek, among other improvements.

Rob Jansen [announced](https://lists.torproject.org/pipermail/tor-dev/2015-February/008317.html) a major new release of [Shadow](https://shadow.github.io/), the Tor network simulation tool. New features include support for running Bitcoin software inside the simulation, client activity modelling using dependency graphs, and much more.

Yaron Goland [updated](https://lists.torproject.org/pipermail/tor-talk/2015-February/036952.html) the [Tor Onion Proxy libary](https://github.com/thaliproject/Tor_Onion_Proxy_Library), a project to “enable Android and Java applications to easily host their own Tor Onion Proxies using the core Tor binaries”. This release incorporates newer software and a simplified build process.

The organizers of the Workshop on Surveillance and Technology issued a [call for papers](https://satsymposium.org/) ahead of their event, which will be held on June 29th. The deadline for submission is midnight UTC on March 11th; please see SAT’s website for topics covered by the workshop and submission guidelines.

Bendert Zevenbergen [relayed](https://lists.torproject.org/pipermail/tor-talk/2015-February/036939.html) another call for participation, this time in the ACM SigComm2015 workshop on “Ethics in Networked Systems Research”.

* * * * *

This issue of Tor Weekly News has been assembled by Harmony and Roger Dingledine.

Want to continue reading TWN? Please help us create this newsletter. We still need more volunteers to watch the Tor community and report important news. Please see the [project page](https://trac.torproject.org/projects/tor/wiki/TorWeeklyNews), write down your name and subscribe to the [team mailing list](https://lists.torproject.org/cgi-bin/mailman/listinfo/news-team) if you want to get involved!
