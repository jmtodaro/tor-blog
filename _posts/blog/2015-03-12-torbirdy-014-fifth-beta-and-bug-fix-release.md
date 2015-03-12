---
layout: post
title: "TorBirdy 0.1.4: Fifth Beta and Bug Fix Release"
permalink: torbirdy-014-fifth-beta-and-bug-fix-release
date: 2015-03-12 10:01:25
author: sukhbir
category: blog
comments: disabled
tags: ["email", "icedove", "Thunderbird", "TorBirdy"]
---

We are happy to announce the release of TorBirdy 0.1.4, our fifth beta release. This is a bug-fix release, which fixes an issue with TorBirdy 0.1.3 that prevents Thunderbird from starting if three or more than three IMAP accounts are configured. This was reported by users in several tickets ([\#14099](https://trac.torproject.org/projects/tor/ticket/14099), [\#13982](https://trac.torproject.org/projects/tor/ticket/13982), [\#13722](https://trac.torproject.org/projects/tor/ticket/13722), [\#14007](https://trac.torproject.org/projects/tor/ticket/14007), [\#14130](https://trac.torproject.org/projects/tor/ticket/14130)) and affects all platforms.

**Changes in TorBirdy 0.1.4**

> 0.1.4, 09 March 2015  
>  \* Fix bug that prevented Thunderbird with TorBirdy 0.1.3 from starting  
>  in profiles with more than three IMAP accounts (closes \#14099, \#13982,  
>  \#13722, \#14007, \#14130)

**Technical Explanation**

This bug was due to a variable in a *for* lop that was declared twice and was affecting the enumeration of an outer loop (lines 521 and 531 in *components/torbirdy.js*) used to iterate over IMAP accounts. Please see commit [625f80e](https://gitweb.torproject.org/torbirdy.git/commit/?id=625f80e1f656f38784c3928cc5e62f1407d1c400) in the TorBirdy repository for the fix.

Users who are not affected by this issue (less than three IMAP accounts configured) may also upgrade but note that this release does not introduce any new features.

We offer two ways of installing TorBirdy -- either by visiting our [website](https://dist.torproject.org/torbirdy/torbirdy-0.1.4.xpi) ([GPG signature](https://dist.torproject.org/torbirdy/torbirdy-0.1.4.xpi.asc)) or by visiting the [Mozilla Add-ons page for TorBirdy](https://addons.mozilla.org/en-us/thunderbird/addon/torbirdy/). (TorBirdy 0.1.4 has been [fully reviewed](https://developer.mozilla.org/en-US/Add-ons/AMO/Policy/Reviews#Full_Review) by Mozilla.)

**Using TorBirdy for the First Time?**

As a general anonymity and security note: we are still working on [two known anonymity issues](https://trac.torproject.org/projects/tor/wiki/torbirdy#InfoLeaks) with Mozilla. Please make sure that you read the [Before Using TorBirdy](https://trac.torproject.org/projects/tor/wiki/torbirdy#BeforeusingTorBirdy) and [Known TorBirdy Issues](https://trac.torproject.org/projects/tor/wiki/torbirdy#KnownTorBirdyIssues) sections on the wiki before using TorBirdy.

We had love help with getting our patches accepted, or anything that you think will help improve TorBirdy!

Feel free to follow along with the release on the [tor-talk](https://lists.torproject.org/pipermail/tor-talk/2015-March/037246.html) mailing list.
