---
layout: post
title: "Tor 0.2.6.4-rc is released"
permalink: tor-0264-rc-released
date: 2015-03-09 20:41:56
author: nickm
category: blog
comments: open
tags: ["release candidate", "tor"]
---

Tor 0.2.6.4-rc fixes an issue in the directory code that an attacker might be able to use in order to crash certain Tor directories. It also resolves some minor issues left over from, or introduced in, Tor 0.2.6.3-alpha or earlier.

If no serious issues are found in this release, the next 0.2.6 release will make 0.2.6 the officially stable branch of Tor.

You can download the source from the usual place on the website. Packages should be up in a few days.

**NOTE:** This is an alpha release. Please expect bugs.

Changes in version 0.2.6.4-rc - 2015-03-09

-   Major bugfixes (crash, OSX, security):
    -   Fix a remote denial-of-service opportunity caused by a bug in OSX's \_strlcat\_chk() function. Fixes bug 15205; bug first appeared in OSX 10.9.
-   Major bugfixes (relay, stability, possible security):
    -   Fix a bug that could lead to a relay crashing with an assertion failure if a buffer of exactly the wrong layout is passed to buf\_pullup() at exactly the wrong time. Fixes bug 15083; bugfix on 0.2.0.10-alpha. Patch from "cypherpunks".
    -   Do not assert if the 'data' pointer on a buffer is advanced to the very end of the buffer; log a BUG message instead. Only assert if it is past that point. Fixes bug 15083; bugfix on 0.2.0.10-alpha.

 

<!-- more -->

-   Major bugfixes (FreeBSD IPFW transparent proxy):
    -   Fix address detection with FreeBSD transparent proxies, when "TransProxyType ipfw" is in use. Fixes bug 15064; bugfix on 0.2.5.4-alpha.
-   Major bugfixes (Linux seccomp2 sandbox):
    -   Pass IPPROTO\_TCP rather than 0 to socket(), so that the Linux seccomp2 sandbox doesn't fail. Fixes bug 14989; bugfix on 0.2.6.3-alpha.
    -   Allow AF\_UNIX hidden services to be used with the seccomp2 sandbox. Fixes bug 15003; bugfix on 0.2.6.3-alpha.
    -   Upon receiving sighup with the seccomp2 sandbox enabled, do not crash during attempts to call wait4. Fixes bug 15088; bugfix on 0.2.5.1-alpha. Patch from "sanic".
-   Minor features (controller):
    -   Messages about problems in the bootstrap process now include information about the server we were trying to connect to when we noticed the problem. Closes ticket 15006.
-   Minor features (geoip):
    -   Update geoip to the March 3 2015 Maxmind GeoLite2 Country database.
    -   Update geoip6 to the March 3 2015 Maxmind GeoLite2 Country database.
-   Minor features (logs):
    -   Quiet some log messages in the heartbeat and at startup. Closes ticket 14950.
-   Minor bugfixes (certificate handling):
    -   If an authority operator accidentally makes a signing certificate with a future publication time, do not discard its real signing certificates. Fixes bug 11457; bugfix on 0.2.0.3-alpha.
    -   Remove any old authority certificates that have been superseded for at least two days. Previously, we would keep superseded certificates until they expired, if they were published close in time to the certificate that superseded them. Fixes bug 11454; bugfix on 0.2.1.8-alpha.
-   Minor bugfixes (compilation):
    -   Fix a compilation warning on s390. Fixes bug 14988; bugfix on 0.2.5.2-alpha.
    -   Fix a compilation warning on FreeBSD. Fixes bug 15151; bugfix on 0.2.6.2-alpha.
-   Minor bugfixes (testing):
    -   Fix endianness issues in unit test for resolve\_my\_address() to have it pass on big endian systems. Fixes bug 14980; bugfix on Tor 0.2.6.3-alpha.
    -   Avoid a side-effect in a tor\_assert() in the unit tests. Fixes bug 15188; bugfix on 0.1.2.3-alpha. Patch from Tom van der Woerdt.
    -   When running the new 'make test-stem' target, use the configured python binary. Fixes bug 15037; bugfix on 0.2.6.3-alpha. Patch from "cypherpunks".
    -   When running the zero-length-keys tests, do not use the default torrc file. Fixes bug 15033; bugfix on 0.2.6.3-alpha. Reported by "reezer".
-   Directory authority IP change:
    -   The directory authority Faravahar has a new IP address. This closes ticket 14487.
-   Removed code:
    -   Remove some lingering dead code that once supported mempools. Mempools were disabled by default in 0.2.5, and removed entirely in 0.2.6.3-alpha. Closes more of ticket 14848; patch by "cypherpunks".

