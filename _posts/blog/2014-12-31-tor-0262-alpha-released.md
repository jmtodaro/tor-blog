---
layout: post
title: "Tor 0.2.6.2-alpha is released"
permalink: tor-0262-alpha-released
date: 2014-12-31 13:28:53
author: nickm
category: blog
comments: open
tags: ["alpha", "tor-release"]
---

Tor 0.2.6.2-alpha is the second alpha release in the 0.2.6.x series. It introduces a major new backend for deciding when to send cells on channels, which should lead down the road to big performance increases. It contains security and statistics features for better work on hidden services, and numerous bugfixes.

This release contains many new unit tests, along with major performance improvements for running testing networks using Chutney. Thanks to a series of patches contributed by "teor", testing networks should now bootstrap in seconds, rather than minutes.

You can download the source from the usual place on the website. Packages should be up in a few days.

**NOTE:** This is an alpha release. Please expect bugs.

Changes in version 0.2.6.2-alpha - 2014-12-31
---------------------------------------------

-   Major features (relay, infrastructure):
    -   Complete revision of the code that relays use to decide which cell to send next. Formerly, we selected the best circuit to write on each channel, but we didn't select among channels in any sophisticated way. Now, we choose the best circuits globally from among those whose channels are ready to deliver traffic.

        This patch implements a new inter-cmux comparison API, a global high/low watermark mechanism and a global scheduler loop for transmission prioritization across all channels as well as among circuits on one channel. This schedule is currently tuned to (tolerantly) avoid making changes in network performance, but it should form the basis for major circuit performance increases in the future. Code by Andrea; tuning by Rob Jansen; implements ticket 9262.

-   Major features (hidden services):
    -   Make HS port scanning more difficult by immediately closing the circuit when a user attempts to connect to a nonexistent port. Closes ticket 13667.
    -   Add a HiddenServiceStatistics option that allows Tor relays to gather and publish statistics about the overall size and volume of hidden service usage. Specifically, when this option is turned on, an HSDir will publish an approximate number of hidden services that have published descriptors to it the past 24 hours. Also, if a relay has acted as a hidden service rendezvous point, it will publish the approximate amount of rendezvous cells it has relayed the past 24 hours. The statistics themselves are obfuscated so that the exact values cannot be derived. For more details see proposal 238, "Better hidden service stats from Tor relays". This feature is currently disabled by default. Implements feature 13192.

 

<!-- more -->

Tor 0.2.6.2-alpha is the second alpha release in the 0.2.6.x series. It introduces a major new backend for deciding when to send cells on channels, which should lead down the road to big performance increases. It contains security and statistics features for better work on hidden services, and numerous bugfixes.

This release contains many new unit tests, along with major performance improvements for running testing networks using Chutney. Thanks to a series of patches contributed by "teor", testing networks should now bootstrap in seconds, rather than minutes.

You can download the source from the usual place on the website. Packages should be up in a few days.

**NOTE:** This is an alpha release. Please expect bugs.

Changes in version 0.2.6.2-alpha - 2014-12-31
---------------------------------------------

-   Major features (relay, infrastructure):
    -   Complete revision of the code that relays use to decide which cell to send next. Formerly, we selected the best circuit to write on each channel, but we didn't select among channels in any sophisticated way. Now, we choose the best circuits globally from among those whose channels are ready to deliver traffic.

        This patch implements a new inter-cmux comparison API, a global high/low watermark mechanism and a global scheduler loop for transmission prioritization across all channels as well as among circuits on one channel. This schedule is currently tuned to (tolerantly) avoid making changes in network performance, but it should form the basis for major circuit performance increases in the future. Code by Andrea; tuning by Rob Jansen; implements ticket 9262.

-   Major features (hidden services):
    -   Make HS port scanning more difficult by immediately closing the circuit when a user attempts to connect to a nonexistent port. Closes ticket 13667.
    -   Add a HiddenServiceStatistics option that allows Tor relays to gather and publish statistics about the overall size and volume of hidden service usage. Specifically, when this option is turned on, an HSDir will publish an approximate number of hidden services that have published descriptors to it the past 24 hours. Also, if a relay has acted as a hidden service rendezvous point, it will publish the approximate amount of rendezvous cells it has relayed the past 24 hours. The statistics themselves are obfuscated so that the exact values cannot be derived. For more details see proposal 238, "Better hidden service stats from Tor relays". This feature is currently disabled by default. Implements feature 13192.

 

-   Major bugfixes (client, automap):
    -   Repair automapping with IPv6 addresses. This automapping should have worked previously, but one piece of debugging code that we inserted to detect a regression actually caused the regression to manifest itself again. Fixes bug 13811 and bug 12831; bugfix on 0.2.4.7-alpha. Diagnosed and fixed by Francisco Blas Izquierdo Riera.
-   Major bugfixes (hidden services):
    -   When closing an introduction circuit that was opened in parallel with others, don't mark the introduction point as unreachable. Previously, the first successful connection to an introduction point would make the other introduction points get marked as having timed out. Fixes bug 13698; bugfix on 0.0.6rc2.
-   Directory authority changes:
    -   Remove turtles as a directory authority.
    -   Add longclaw as a new (v3) directory authority. This implements ticket 13296. This keeps the directory authority count at 9.
-   Major removed features:
    -   Tor clients no longer support connecting to hidden services running on Tor 0.2.2.x and earlier; the Support022HiddenServices option has been removed. (There shouldn't be any hidden services running these versions on the network.) Closes ticket 7803.
-   Minor features (client):
    -   Validate hostnames in SOCKS5 requests more strictly. If SafeSocks is enabled, reject requests with IP addresses as hostnames. Resolves ticket 13315.
-   Minor features (controller):
    -   Add a "SIGNAL HEARTBEAT" controller command that tells Tor to write an unscheduled heartbeat message to the log. Implements feature 9503.
-   Minor features (geoip):
    -   Update geoip and geoip6 to the November 15 2014 Maxmind GeoLite2 Country database.
-   Minor features (hidden services):
    -   When re-enabling the network, don't try to build introduction circuits until we have successfully built a circuit. This makes hidden services come up faster when the network is re-enabled. Patch from "akwizgran". Closes ticket 13447.
    -   When we fail to a retrieve hidden service descriptor, send the controller an "HS\_DESC FAILED" controller event. Implements feature 13212.
    -   New HiddenServiceDirGroupReadable option to cause hidden service directories and hostname files to be created group-readable. Patch from "anon", David Stainton, and "meejah". Closes ticket 11291.
-   Minor features (systemd):
    -   Where supported, when running with systemd, report successful startup to systemd. Part of ticket 11016. Patch by Michael Scherer.
    -   When running with systemd, support systemd watchdog messages. Part of ticket 11016. Patch by Michael Scherer.
-   Minor features (transparent proxy):
    -   Update the transparent proxy option checks to allow for both ipfw and pf on OS X. Closes ticket 14002.
    -   Use the correct option when using IPv6 with transparent proxy support on Linux. Resolves 13808. Patch by Francisco Blas Izquierdo Riera.
-   Minor bugfixes (preventative security, C safety):
    -   When reading a hexadecimal, base-32, or base-64 encoded value from a string, always overwrite the whole output buffer. This prevents some bugs where we would look at (but fortunately, not reveal) uninitialized memory on the stack. Fixes bug 14013; bugfix on all versions of Tor.
    -   Clear all memory targetted by tor\_addr\_{to,from}\_sockaddr(), not just the part that's used. This makes it harder for data leak bugs to occur in the event of other programming failures. Resolves ticket 14041.
-   Minor bugfixes (client, microdescriptors):
    -   Use a full 256 bits of the SHA256 digest of a microdescriptor when computing which microdescriptors to download. This keeps us from erroneous download behavior if two microdescriptor digests ever have the same first 160 bits. Fixes part of bug 13399; bugfix on 0.2.3.1-alpha.
    -   Reset a router's status if its microdescriptor digest changes, even if the first 160 bits remain the same. Fixes part of bug 13399; bugfix on 0.2.3.1-alpha.
-   Minor bugfixes (compilation):
    -   Silence clang warnings under --enable-expensive-hardening, including implicit truncation of 64 bit values to 32 bit, const char assignment to self, tautological compare, and additional parentheses around equality tests. Fixes bug 13577; bugfix on 0.2.5.4-alpha.
    -   Fix a clang warning about checking whether an address in the middle of a structure is NULL. Fixes bug 14001; bugfix on 0.2.1.2-alpha.
-   Minor bugfixes (hidden services):
    -   Correctly send a controller event when we find that a rendezvous circuit has finished. Fixes bug 13936; bugfix on 0.1.1.5-alpha.
    -   Pre-check directory permissions for new hidden-services to avoid at least one case of "Bug: Acting on config options left us in a broken state. Dying." Fixes bug 13942; bugfix on 0.0.6pre1.
    -   When adding a new hidden service (for example, via SETCONF), Tor no longer congratulates the user for running a relay. Fixes bug 13941; bugfix on 0.2.6.1-alpha.
    -   When fetching hidden service descriptors, we now check not only for whether we got the hidden service we had in mind, but also whether we got the particular descriptors we wanted. This prevents a class of inefficient but annoying DoS attacks by hidden service directories. Fixes bug 13214; bugfix on 0.2.1.6-alpha. Reported by "special".
-   Minor bugfixes (Linux seccomp2 sandbox):
    -   Make transparent proxy support work along with the seccomp2 sandbox. Fixes part of bug 13808; bugfix on 0.2.5.1-alpha. Patch by Francisco Blas Izquierdo Riera.
    -   Fix a memory leak in tor-resolve when running with the sandbox enabled. Fixes bug 14050; bugfix on 0.2.5.9-rc.
-   Minor bugfixes (logging):
    -   Downgrade warnings about RSA signature failures to info log level. Emit a warning when an extra info document is found incompatible with a corresponding router descriptor. Fixes bug 9812; bugfix on 0.0.6rc3.
    -   Make connection\_ap\_handshake\_attach\_circuit() log the circuit ID correctly. Fixes bug 13701; bugfix on 0.0.6.
-   Minor bugfixes (misc):
    -   Stop allowing invalid address patterns like "\*/24" that contain both a wildcard address and a bit prefix length. This affects all our address-range parsing code. Fixes bug 7484; bugfix on 0.0.2pre14.
-   Minor bugfixes (testing networks, fast startup):
    -   Allow Tor to build circuits using a consensus with no exits. If the consensus has no exits (typical of a bootstrapping test network), allow Tor to build circuits once enough descriptors have been downloaded. This assists in bootstrapping a testing Tor network. Fixes bug 13718; bugfix on 0.2.4.10-alpha. Patch by "teor".
    -   When V3AuthVotingInterval is low, give a lower If-Modified-Since header to directory servers. This allows us to obtain consensuses promptly when the consensus interval is very short. This assists in bootstrapping a testing Tor network. Fixes parts of bugs 13718 and 13963; bugfix on 0.2.0.3-alpha. Patch by "teor".
    -   Stop assuming that private addresses are local when checking reachability in a TestingTorNetwork. Instead, when testing, assume all OR connections are remote. (This is necessary due to many test scenarios running all relays on localhost.) This assists in bootstrapping a testing Tor network. Fixes bug 13924; bugfix on 0.1.0.1-rc. Patch by "teor".
    -   Avoid building exit circuits from a consensus with no exits. Now thanks to our fix for 13718, we accept a no-exit network as not wholly lost, but we need to remember not to try to build exit circuits on it. Closes ticket 13814; patch by "teor".
    -   Stop requiring exits to have non-zero bandwithcapacity in a TestingTorNetwork. Instead, when TestingMinExitFlagThreshold is 0, ignore exit bandwidthcapacity. This assists in bootstrapping a testing Tor network. Fixes parts of bugs 13718 and 13839; bugfix on 0.2.0.3-alpha. Patch by "teor".
    -   Add "internal" to some bootstrap statuses when no exits are available. If the consensus does not contain Exits, Tor will only build internal circuits. In this case, relevant statuses will contain the word "internal" as indicated in the Tor control- spec.txt. When bootstrap completes, Tor will be ready to build internal circuits. If a future consensus contains Exits, exit circuits may become available. Fixes part of bug 13718; bugfix on 0.2.4.10-alpha. Patch by "teor".
    -   Decrease minimum consensus interval to 10 seconds when TestingTorNetwork is set, or 5 seconds for the first consensus. Fix assumptions throughout the code that assume larger intervals. Fixes bugs 13718 and 13823; bugfix on 0.2.0.3-alpha. Patch by "teor".
    -   Avoid excluding guards from path building in minimal test networks, when we're in a test network and excluding guards would exclude all relays. This typically occurs in incredibly small tor networks, and those using "TestingAuthVoteGuard \*". Fixes part of bug 13718; bugfix on 0.1.1.11-alpha. Patch by "teor".
-   Code simplification and refactoring:
    -   Stop using can\_complete\_circuits as a global variable; access it with a function instead.
    -   Avoid using operators directly as macro arguments: this lets us apply coccinelle transformations to our codebase more directly. Closes ticket 13172.
    -   Combine the functions used to parse ClientTransportPlugin and ServerTransportPlugin into a single function. Closes ticket 6456.
    -   Add inline functions and convenience macros for inspecting channel state. Refactor the code to use convenience macros instead of checking channel state directly. Fixes issue 7356.
    -   Document all members of was\_router\_added\_t and rename ROUTER\_WAS\_NOT\_NEW to ROUTER\_IS\_ALREADY\_KNOWN to make it less confusable with ROUTER\_WAS\_TOO\_OLD. Fixes issue 13644.
    -   In connection\_exit\_begin\_conn(), use END\_CIRC\_REASON\_TORPROTOCOL constant instead of hardcoded value. Fixes issue 13840.
    -   Refactor our generic strmap and digestmap types into a single implementation, so that we can add a new digest256map type trivially.
-   Documentation:
    -   Document the bridge-authority-only 'networkstatus-bridges' file. Closes ticket 13713; patch from "tom".
    -   Fix typo in PredictedPortsRelevanceTime option description in manpage. Resolves issue 13707.
    -   Stop suggesting that users specify relays by nickname: it isn't a good idea. Also, properly cross-reference how to specify relays in all parts of manual documenting options that take a list of relays. Closes ticket 13381.
    -   Clarify the HiddenServiceDir option description in manpage to make it clear that relative paths are taken with respect to the current working directory. Also clarify that this behavior is not guaranteed to remain indefinitely. Fixes issue 13913.
-   Testing:
    -   New tests for many parts of channel, relay, and circuitmux functionality. Code by Andrea; part of 9262.
    -   New tests for parse\_transport\_line(). Part of ticket 6456.
    -   In the unit tests, use chgrp() to change the group of the unit test temporary directory to the current user, so that the sticky bit doesn't interfere with tests that check directory groups. Closes 13678.
    -   Add unit tests for resolve\_my\_addr(). Part of ticket 12376; patch by 'rl1987'.

