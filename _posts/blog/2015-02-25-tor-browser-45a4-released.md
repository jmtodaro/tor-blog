---
layout: post
title: "Tor Browser 4.5a4 is released"
permalink: tor-browser-45a4-released
date: 2015-02-25 19:20:45
author: mikeperry
category: blog
comments: open
tags: ["tbb", "tbb-4.5", "tor browser", "tor browser bundle"]
---

The Tor Browser team is proud to announce the release of the fourth alpha of the 4.5 series of Tor Browser. The release is available from the [extended downloads page](https://www.torproject.org/projects/torbrowser.html.en#downloads-alpha) and also from our [distribution directory](https://www.torproject.org/dist/torbrowser/4.5a4/).

Tor Browser 4.5a4 is based on Firefox ESR 31.5.0, which features [important security updates](https://www.mozilla.org/security/known-vulnerabilities/firefoxESR.html#firefoxesr31.5) to Firefox. Moreover, this release includes an updated Tor, 0.2.6.3-alpha, and switches Scramblesuit and obfs3 bridge support to a new golang-based implementation. We are especially interested in hearing any issues with using obfs3, obfs4, and Scramblesuit in this release.

The release also features several improvements to usability, following the results of the [usability sprint](https://blog.torproject.org/blog/ux-sprint-2015-wrapup) at the end of last month. In particular, the Torbutton onion menu and related preference windows have been overhauled to provide more simplicity and more focus. The onion menu now features a much requested "New Circuit for this site" option, and the security and privacy settings window have been simplified. For censored users, the first run configuration wizard was also improved to present the choice of Pluggable Transport before the local proxy information, in an effort to avoid confusion between Pluggable Transports and local proxies. As can be seen from the changelog below, the release contains several other usability tweaks and enhancements as well.

Here is the full changelog for changes since 4.5-alpha-3:

-   All Platforms
    -   Update Firefox to 31.5.0esr
    -   Update Tor to 0.2.6.3-alpha
    -   Update OpenSSL to 1.0.1l
    -   Update NoScript to 2.6.9.15
    -   Update obfs4proxy to 0.0.4
        -   Use obfs4proxy for ScrambleSuit bridges
    -   Update Torbutton to 1.9.0.0
        -   Bug 13882: Fix display of bridges after bridge settings have been changed
        -   Bug 5698: Use "Tor Browser" branding in "About Tor Browser" dialog
        -   Bug 10280: Strings and pref for preventing plugin initialization.
        -   Bug 14866: Show correct circuit when more than one exists for a given domain
        -   Bug 9442: Add New Circuit button to Torbutton menu
        -   Bug 9906: Warn users before closing all windows and performing new identity.
        -   Bug 8400: Prompt for restart if disk records are enabled/disabled.
        -   Bug 14630: Hide Torbutton's proxy settings tab.
        -   Bug 14632: Disable Cookie Manager until we get it working.
        -   Bug 11175: Remove "About Torbutton" from onion menu.
        -   Bug 13900: Remove remaining SafeCache code in favor of C++ patch
        -   Bug 14490: Use Disconnect search in about:tor search box
        -   Bug 14392: Don't steal input focus in about:tor search box
        -   Bug 11236: Don't set omnibox order in Torbutton (to prevent translation)
        -   Bug 13406: Stop directing users to download-easy.html.en on update
        -   Bug 9387: Handle "custom" mode better in Security Slider
        -   Bug 12430: Bind jar: pref to Security Slider
        -   Bug 14448: Restore Torbutton menu operation on non-English localizations
        -   Translation updates
    -   Update Tor Launcher to 0.2.7.2
        -   Bug 13271: Display Bridge Configuration wizard pane before Proxy pane
        -   Bug 14336: Fix navigation button display issues on some wizard panes
        -   Translation updates
    -   Bug 14203: Prevent meek from displaying an extra update notification
    -   Bug 14849: Remove new NoScript menu option to make permissions permanent
    -   Bug 14851: Set NoScript pref to disable permanent permissions
    -   Bug 14490: Make Disconnect the default omnibox search engine
    -   Bug 11236: Fix omnibox order for non-English builds
        -   Also remove Amazon, eBay and bing; add Youtube and Twitter
    -   Bug 10280: Don't load any plugins into the address space.
    -   Bug 14392: Make about:tor hide itself from the URL bar
    -   Bug 12430: Provide a preference to disable remote jar: urls
    -   Bug 13900: Remove 3rd party HTTP auth tokens via Firefox patch
    -   Bug 5698: Fix branding in "About Torbrowser" window
-   Windows:
    -   Bug 13169: Don't use /dev/random on Windows for SSP
-   Linux:
    -   Bug 13717: Make sure we use the bash shell on Linux

**Note:** Once again, the individual bundles of both Tor Browser series are signed by one of the subkeys of the Tor Browser Developers signing key from now on. You can find its fingerprint on the [Signing Keys](https://www.torproject.org/docs/signing-keys.html.en) page. It is:

    pub   4096R/0x4E2C6E8793298290 2014-12-15
          Key fingerprint = EF6E 286D DA85 EA2A 4BA7
                            DE68 4E2C 6E87 9329 8290
