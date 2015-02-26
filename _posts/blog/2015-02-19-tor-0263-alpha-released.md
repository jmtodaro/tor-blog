---
layout: post
title: "Tor 0.2.6.3-alpha is released"
permalink: tor-0263-alpha-released
date: 2015-02-19 17:32:29
author: nickm
category: blog
comments: open
tags: ["0263", "source-release", "tor-alpha", "tor-dev"]
---

Tor 0.2.6.3-alpha is the third (and hopefully final) alpha release in the 0.2.6.x series. It introduces support for more kinds of sockets, makes it harder to accidentally run an exit, improves our multithreading backend, incorporates several fixes for the AutomapHostsOnResolve option, and fixes numerous other bugs besides.

If no major regressions or security holes are found in this version, the next version will be a release candidate.

You can download the source from the usual place on the website. Packages should be up in a few days.

**NOTE**: This is an alpha release. Please expect bugs.

Changes in version 0.2.6.3-alpha - 2015-02-19

-   Deprecated versions:
    -   Tor relays older than 0.2.4.18-rc are no longer allowed to advertise themselves on the network. Closes ticket 13555.
-   Major features (security, unix domain sockets):
    -   Allow SocksPort to be an AF\_UNIX Unix Domain Socket. Now high risk applications can reach Tor without having to create AF\_INET or AF\_INET6 sockets, meaning they can completely disable their ability to make non-Tor network connections. To create a socket of this type, use "SocksPort unix:/path/to/socket". Implements ticket 12585.
    -   Support mapping hidden service virtual ports to AF\_UNIX sockets. The syntax is "HiddenServicePort 80 unix:/path/to/socket". Implements ticket 11485.

 

<!-- more -->

Tor 0.2.6.3-alpha is the third (and hopefully final) alpha release in the 0.2.6.x series. It introduces support for more kinds of sockets, makes it harder to accidentally run an exit, improves our multithreading backend, incorporates several fixes for the AutomapHostsOnResolve option, and fixes numerous other bugs besides.

If no major regressions or security holes are found in this version, the next version will be a release candidate.

You can download the source from the usual place on the website. Packages should be up in a few days.

**NOTE**: This is an alpha release. Please expect bugs.

Changes in version 0.2.6.3-alpha - 2015-02-19

-   Deprecated versions:
    -   Tor relays older than 0.2.4.18-rc are no longer allowed to advertise themselves on the network. Closes ticket 13555.
-   Major features (security, unix domain sockets):
    -   Allow SocksPort to be an AF\_UNIX Unix Domain Socket. Now high risk applications can reach Tor without having to create AF\_INET or AF\_INET6 sockets, meaning they can completely disable their ability to make non-Tor network connections. To create a socket of this type, use "SocksPort unix:/path/to/socket". Implements ticket 12585.
    -   Support mapping hidden service virtual ports to AF\_UNIX sockets. The syntax is "HiddenServicePort 80 unix:/path/to/socket". Implements ticket 11485.

 

-   Major features (changed defaults):
    -   Prevent relay operators from unintentionally running exits: When a relay is configured as an exit node, we now warn the user unless the "ExitRelay" option is set to 1. We warn even more loudly if the relay is configured with the default exit policy, since this can indicate accidental misconfiguration. Setting "ExitRelay 0" stops Tor from running as an exit relay. Closes ticket 10067.
-   Major features (directory system):
    -   When downloading server- or microdescriptors from a directory server, we no longer launch multiple simultaneous requests to the same server. This reduces load on the directory servers, especially when directory guards are in use. Closes ticket 9969.
    -   When downloading server- or microdescriptors over a tunneled connection, do not limit the length of our requests to what the Squid proxy is willing to handle. Part of ticket 9969.
    -   Authorities can now vote on the correct digests and latest versions for different software packages. This allows packages that include Tor to use the Tor authority system as a way to get notified of updates and their correct digests. Implements proposal 227. Closes ticket 10395.
-   Major features (performance):
    -   Make the CPU worker implementation more efficient by avoiding the kernel and lengthening pipelines. The original implementation used sockets to transfer data from the main thread to the workers, and didn't allow any thread to be assigned more than a single piece of work at once. The new implementation avoids communications overhead by making requests in shared memory, avoiding kernel IO where possible, and keeping more requests in flight at once. Implements ticket 9682.
-   Major features (relay):
    -   Raise the minimum acceptable configured bandwidth rate for bridges to 50 KiB/sec and for relays to 75 KiB/sec. (The old values were 20 KiB/sec.) Closes ticket 13822.
-   Major bugfixes (exit node stability):
    -   Fix an assertion failure that could occur under high DNS load. Fixes bug 14129; bugfix on Tor 0.0.7rc1. Found by "jowr"; diagnosed and fixed by "cypherpunks".
-   Major bugfixes (mixed relay-client operation):
    -   When running as a relay and client at the same time (not recommended), if we decide not to use a new guard because we want to retry older guards, only close the locally-originating circuits passing through that guard. Previously we would close all the circuits through that guard. Fixes bug 9819; bugfix on 0.2.1.1-alpha. Reported by "skruffy".
-   Minor features (build):
    -   New --disable-system-torrc compile-time option to prevent Tor from looking for the system-wide torrc or torrc-defaults files. Resolves ticket 13037.
-   Minor features (controller):
    -   Include SOCKS\_USERNAME and SOCKS\_PASSWORD values in controller events so controllers can observe circuit isolation inputs. Closes ticket 8405.
    -   ControlPort now supports the unix:/path/to/socket syntax as an alternative to the ControlSocket option, for consistency with SocksPort and HiddenServicePort. Closes ticket 14451.
    -   New "GETINFO bw-event-cache" to get information about recent bandwidth events. Closes ticket 14128. Useful for controllers to get recent bandwidth history after the fix for ticket 13988.
-   Minor features (Denial of service resistance):
    -   Count the total number of bytes used storing hidden service descriptors against the value of MaxMemInQueues. If we're low on memory, and more than 20% of our memory is used holding hidden service descriptors, free them until no more than 10% of our memory holds hidden service descriptors. Free the least recently fetched descriptors first. Resolves ticket 13806.
    -   When we have recently been under memory pressure (over 3/4 of MaxMemInQueues is allocated), then allocate smaller zlib objects for small requests. Closes ticket 11791.
-   Minor features (geoip):
    -   Update geoip and geoip6 files to the January 7 2015 Maxmind GeoLite2 Country database.
-   Minor features (guard nodes):
    -   Reduce the time delay before saving guard status to disk from 10 minutes to 30 seconds (or from one hour to 10 minutes if AvoidDiskWrites is set). Closes ticket 12485.
-   Minor features (hidden service):
    -   Make Sybil attacks against hidden services harder by changing the minimum time required to get the HSDir flag from 25 hours up to 96 hours. Addresses ticket 14149.
    -   New option "HiddenServiceAllowUnknownPorts" to allow hidden services to disable the anti-scanning feature introduced in 0.2.6.2-alpha. With this option not set, a connection to an unlisted port closes the circuit. With this option set, only a RELAY\_DONE cell is sent. Closes ticket 14084.
-   Minor features (interface):
    -   Implement "-f -" command-line option to read torrc configuration from standard input, if you don't want to store the torrc file in the file system. Implements feature 13865.
-   Minor features (logging):
    -   Add a count of unique clients to the bridge heartbeat message. Resolves ticket 6852.
    -   Suppress "router info incompatible with extra info" message when reading extrainfo documents from cache. (This message got loud around when we closed bug 9812 in 0.2.6.2-alpha.) Closes ticket 13762.
    -   Elevate hidden service authorized-client message from DEBUG to INFO. Closes ticket 14015.
-   Minor features (stability):
    -   Add assertions in our hash-table iteration code to check for corrupted values that could cause infinite loops. Closes ticket 11737.
-   Minor features (systemd):
    -   Various improvements and modernizations in systemd hardening support. Closes ticket 13805. Patch from Craig Andrews.
-   Minor features (testing networks):
    -   Drop the minimum RendPostPeriod on a testing network to 5 seconds, and the default on a testing network to 2 minutes. Drop the MIN\_REND\_INITIAL\_POST\_DELAY on a testing network to 5 seconds, but keep the default on a testing network at 30 seconds. This reduces HS bootstrap time to around 25 seconds. Also, change the default time in test-network.sh to match. Closes ticket 13401. Patch by "teor".
    -   Create TestingDirAuthVoteHSDir to correspond to TestingDirAuthVoteExit/Guard. Ensures that authorities vote the HSDir flag for the listed relays regardless of uptime or ORPort connectivity. Respects the value of VoteOnHidServDirectoriesV2. Partial implementation for ticket 14067. Patch by "teor".
-   Minor features (tor2web mode):
    -   Introduce the config option Tor2webRendezvousPoints, which allows clients in Tor2webMode to select a specific Rendezvous Point to be used in HS circuits. This might allow better performance for Tor2Web nodes. Implements ticket 12844.
-   Minor bugfixes (client DNS):
    -   Report the correct cached DNS expiration times on SOCKS port or in DNS replies. Previously, we would report everything as "never expires." Fixes bug 14193; bugfix on 0.2.3.17-beta.
    -   Avoid a small memory leak when we find a cached answer for a reverse DNS lookup in a client-side DNS cache. (Remember, client- side DNS caching is off by default, and is not recommended.) Fixes bug 14259; bugfix on 0.2.0.1-alpha.
-   Minor bugfixes (client, automapping):
    -   Avoid crashing on torrc lines for VirtualAddrNetworkIPv[4|6] when no value follows the option. Fixes bug 14142; bugfix on 0.2.4.7-alpha. Patch by "teor".
    -   Fix a memory leak when using AutomapHostsOnResolve. Fixes bug 14195; bugfix on 0.1.0.1-rc.
    -   Prevent changes to other options from removing the wildcard value "." from "AutomapHostsSuffixes". Fixes bug 12509; bugfix on 0.2.0.1-alpha.
    -   Allow MapAddress and AutomapHostsOnResolve to work together when an address is mapped into another address type (like .onion) that must be automapped at resolve time. Fixes bug 7555; bugfix on 0.2.0.1-alpha.
-   Minor bugfixes (client, bridges):
    -   When we are using bridges and we had a network connectivity problem, only retry connecting to our currently configured bridges, not all bridges we know about and remember using. Fixes bug 14216; bugfix on 0.2.2.17-alpha.
-   Minor bugfixes (client, IPv6):
    -   Reject socks requests to literal IPv6 addresses when IPv6Traffic flag is not set; and not because the NoIPv4Traffic flag was set. Previously we'd looked at the NoIPv4Traffic flag for both types of literal addresses. Fixes bug 14280; bugfix on 0.2.4.7-alpha.
-   Minor bugfixes (compilation):
    -   The address of an array in the middle of a structure will always be non-NULL. clang recognises this and complains. Disable the tautologous and redundant check to silence this warning. Fixes bug 14001; bugfix on 0.2.1.2-alpha.
    -   Avoid warnings when building with systemd 209 or later. Fixes bug 14072; bugfix on 0.2.6.2-alpha. Patch from "h.venev".
    -   Compile correctly with (unreleased) OpenSSL 1.1.0 headers. Addresses ticket 14188.
    -   Build without warnings with the stock OpenSSL srtp.h header, which has a duplicate declaration of SSL\_get\_selected\_srtp\_profile(). Fixes bug 14220; this is OpenSSL's bug, not ours.
    -   Do not compile any code related to Tor2Web mode when Tor2Web mode is not enabled at compile time. Previously, this code was included in a disabled state. See discussion on ticket 12844.
    -   Remove the --disable-threads configure option again. It was accidentally partially reintroduced in 29ac883606d6d. Fixes bug 14819; bugfix on 0.2.6.2-alpha.
-   Minor bugfixes (controller):
    -   Report "down" in response to the "GETINFO entry-guards" command when relays are down with an unreachable\_since value. Previously, we would report "up". Fixes bug 14184; bugfix on 0.1.2.2-alpha.
    -   Avoid crashing on a malformed EXTENDCIRCUIT command. Fixes bug 14116; bugfix on 0.2.2.9-alpha.
    -   Add a code for the END\_CIRC\_REASON\_IP\_NOW\_REDUNDANT circuit close reason. Fixes bug 14207; bugfix on 0.2.6.2-alpha.
-   Minor bugfixes (directory authority):
    -   Allow directory authorities to fetch more data from one another if they find themselves missing lots of votes. Previously, they had been bumping against the 10 MB queued data limit. Fixes bug 14261; bugfix on 0.1.2.5-alpha.
    -   Do not attempt to download extrainfo documents which we will be unable to validate with a matching server descriptor. Fixes bug 13762; bugfix on 0.2.0.1-alpha.
    -   Fix a bug that was truncating AUTHDIR\_NEWDESC events sent to the control port. Fixes bug 14953; bugfix on 0.2.0.1-alpha.
    -   Enlarge the buffer to read bwauth generated files to avoid an issue when parsing the file in dirserv\_read\_measured\_bandwidths(). Fixes bug 14125; bugfix on 0.2.2.1-alpha.
-   Minor bugfixes (file handling):
    -   Stop failing when key files are zero-length. Instead, generate new keys, and overwrite the empty key files. Fixes bug 13111; bugfix on all versions of Tor. Patch by "teor".
    -   Stop generating a fresh .old RSA onion key file when the .old file is missing. Fixes part of 13111; bugfix on 0.0.6rc1.
    -   Avoid overwriting .old key files with empty key files.
    -   Skip loading zero-length extrainfo store, router store, stats, state, and key files.
    -   Avoid crashing when trying to reload a torrc specified as a relative path with RunAsDaemon turned on. Fixes bug 13397; bugfix on 0.2.3.11-alpha.
-   Minor bugfixes (hidden services):
    -   Close the introduction circuit when we have no more usable intro points, instead of waiting for it to time out. This also ensures that no follow-up HS descriptor fetch is triggered when the circuit eventually times out. Fixes bug 14224; bugfix on 0.0.6.
    -   When fetching a hidden service descriptor for a down service that was recently up, do not keep refetching until we try the same replica twice in a row. Fixes bug 14219; bugfix on 0.2.0.10-alpha.
    -   Successfully launch Tor with a nonexistent hidden service directory. Our fix for bug 13942 didn't catch this case. Fixes bug 14106; bugfix on 0.2.6.2-alpha.
-   Minor bugfixes (logging):
    -   Avoid crashing when there are more log domains than entries in domain\_list. Bugfix on 0.2.3.1-alpha.
    -   Add a string representation for LD\_SCHED. Fixes bug 14740; bugfix on 0.2.6.1-alpha.
    -   Don't log messages to stdout twice when starting up. Fixes bug 13993; bugfix on 0.2.6.1-alpha.
-   Minor bugfixes (parsing):
    -   Stop accepting milliseconds (or other junk) at the end of descriptor publication times. Fixes bug 9286; bugfix on 0.0.2pre25.
    -   Support two-number and three-number version numbers correctly, in case we change the Tor versioning system in the future. Fixes bug 13661; bugfix on 0.0.8pre1.
-   Minor bugfixes (path counting):
    -   When deciding whether the consensus lists any exit nodes, count the number listed in the consensus, not the number we have descriptors for. Fixes part of bug 14918; bugfix on 0.2.6.2-alpha.
    -   When deciding whether we have any exit nodes, only examine ExitNodes when the ExitNodes option is actually set. Fixes part of bug 14918; bugfix on 0.2.6.2-alpha.
    -   Get rid of redundant and possibly scary warnings that we are missing directory information while we bootstrap. Fixes part of bug 14918; bugfix on 0.2.6.2-alpha.
-   Minor bugfixes (portability):
    -   Fix the ioctl()-based network interface lookup code so that it will work on systems that have variable-length struct ifreq, for example Mac OS X.
    -   Fix scheduler compilation on targets where char is unsigned. Fixes bug 14764; bugfix on 0.2.6.2-alpha. Reported by Christian Kujau.
-   Minor bugfixes (sandbox):
    -   Allow glibc fatal errors to be sent to stderr before Tor exits. Previously, glibc would try to write them to /dev/tty, and the sandbox would trap the call and make Tor exit prematurely. Fixes bug 14759; bugfix on 0.2.5.1-alpha.
-   Minor bugfixes (shutdown):
    -   When shutting down, always call event\_del() on lingering read or write events before freeing them. Otherwise, we risk double-frees or read-after-frees in event\_base\_free(). Fixes bug 12985; bugfix on 0.1.0.2-rc.
-   Minor bugfixes (small memory leaks):
    -   Avoid leaking memory when using IPv6 virtual address mappings. Fixes bug 14123; bugfix on 0.2.4.7-alpha. Patch by Tom van der Woerdt.
-   Minor bugfixes (statistics):
    -   Increase period over which bandwidth observations are aggregated from 15 minutes to 4 hours. Fixes bug 13988; bugfix on 0.0.8pre1.
-   Minor bugfixes (systemd support):
    -   Fix detection and operation of systemd watchdog. Fixes part of bug 14141; bugfix on 0.2.6.2-alpha. Patch from Tomasz Torcz.
    -   Run correctly under systemd with the RunAsDaemon option set. Fixes part of bug 14141; bugfix on 0.2.5.7-rc. Patch from Tomasz Torcz.
    -   Inform the systemd supervisor about more changes in the Tor process status. Implements part of ticket 14141. Patch from Tomasz Torcz.
    -   Cause the "--disable-systemd" option to actually disable systemd support. Fixes bug 14350; bugfix on 0.2.6.2-alpha. Patch from "blueness".
-   Minor bugfixes (TLS):
    -   Check more thoroughly throughout the TLS code for possible unlogged TLS errors. Possible diagnostic or fix for bug 13319.
-   Minor bugfixes (transparent proxy):
    -   Use getsockname, not getsockopt, to retrieve the address for a TPROXY-redirected connection. Fixes bug 13796; bugfix on 0.2.5.2-alpha.
-   Code simplification and refactoring:
    -   Move fields related to isolating and configuring client ports into a shared structure. Previously, they were duplicated across port\_cfg\_t, listener\_connection\_t, and edge\_connection\_t. Failure to copy them correctly had been the cause of at least one bug in the past. Closes ticket 8546.
    -   Refactor the get\_interface\_addresses\_raw() doom-function into multiple smaller and simpler subfunctions. Cover the resulting subfunctions with unit-tests. Fixes a significant portion of issue 12376.
    -   Remove workaround in dirserv\_thinks\_router\_is\_hs\_dir() that was only for version \<= 0.2.2.24 which is now deprecated. Closes ticket 14202.
    -   Remove a test for a long-defunct broken version-one directory server.
-   Documentation:
    -   Adding section on OpenBSD to our TUNING document. Thanks to mmcc for writing the OpenBSD-specific tips. Resolves ticket 13702.
    -   Make the tor-resolve documentation match its help string and its options. Resolves part of ticket 14325.
    -   Log a more useful error message from tor-resolve when failing to look up a hidden service address. Resolves part of ticket 14325.
-   Downgraded warnings:
    -   Don't warn when we've attempted to contact a relay using the wrong ntor onion key. Closes ticket 9635.
-   Removed features:
    -   To avoid confusion with the "ExitRelay" option, "ExitNode" is no longer silently accepted as an alias for "ExitNodes".
    -   The --enable-mempool and --enable-buf-freelists options, which were originally created to work around bad malloc implementations, no longer exist. They were off-by-default in 0.2.5. Closes ticket 14848.
-   Testing:
    -   Make the checkdir/perms test complete successfully even if the global umask is not 022. Fixes bug 14215; bugfix on 0.2.6.2-alpha.
    -   Test that tor does not fail when key files are zero-length. Check that tor generates new keys, and overwrites the empty key files.
    -   Test that tor generates new keys when keys are missing (existing behavior).
    -   Test that tor does not overwrite key files that already contain data (existing behavior). Tests bug 13111. Patch by "teor".
    -   New "make test-stem" target to run stem integration tests. Requires that the "STEM\_SOURCE\_DIR" environment variable be set. Closes ticket 14107.
    -   Make the test\_cmdline\_args.py script work correctly on Windows. Patch from Gisle Vanem.
    -   Move the slower unit tests into a new "./src/test/test-slow" binary that can be run independently of the other tests. Closes ticket 13243.
    -   Avoid undefined behavior when sampling huge values from the Laplace distribution. This made unittests fail on Raspberry Pi. Bug found by Device. Fixes bug 14090; bugfix on 0.2.6.2-alpha.

