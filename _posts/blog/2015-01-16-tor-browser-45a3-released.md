---
layout: post
title: "Tor Browser 4.5a3 is released"
permalink: tor-browser-45a3-released
date: 2015-01-16 10:37:44
author: gk
category: blog
comments: open
tags: ["tbb", "tbb-4.5", "tor browser", "tor browser bundle"]
---

The third alpha release of the 4.5 series is available from the [extended downloads page](https://www.torproject.org/projects/torbrowser.html.en#downloads-alpha) and also from our [distribution directory](https://www.torproject.org/dist/torbrowser/4.5a3/).

**Note:** The individual bundles of the alpha series are signed by one of the subkeys of the Tor Browser Developers signing key from now on. You can find its fingerprint on the [Signing Keys](https://www.torproject.org/docs/signing-keys.html.en) page. It is:

    pub   4096R/0x4E2C6E8793298290 2014-12-15
          Key fingerprint = EF6E 286D DA85 EA2A 4BA7
                            DE68 4E2C 6E87 9329 8290

Tor Browser 4.5a3 is based on Firefox ESR 31.4.0, which features [important security updates](https://www.mozilla.org/security/known-vulnerabilities/firefoxESR.html#firefoxesr31.4) to Firefox. Its updater now contains the code for verifying signed update files and does not accept unsigned ones anymore. Moreover, this release includes an updated Tor, 0.2.6.2-alpha, an updated meek, 0.15, which is now working again, and a bunch of additional improvements and bugfixes.

Here is the changelog since 4.5-alpha-2:

-   All Platforms
    -   Update Firefox to 31.4.0esr
    -   Update Tor to 0.2.6.2-alpha
    -   Update NoScript to 2.6.9.10
    -   Update HTTPS Everywhere to 5.0developement.2
    -   Update meek to 0.15
    -   Update Torbutton to 1.8.1.3
        -   Bug 13998: Handle changes in NoScript 2.6.9.8+
        -   Bug 14100: Option to hide NetworkSettings menuitem
        -   Bug 13079: Option to skip control port verification
        -   Bug 13835: Option to change default Tor Browser homepage
        -   Bug 11449: Fix new identity error if NoScript is not enabled
        -   Bug 13881: Localize strings for tor circuit display
        -   Bug 9387: Incorporate user feedback
        -   Bug 13671: Fixup for circuit display if bridges are used
        -   Translation updates
    -   Update Tor Launcher 0.2.7.1
        -   Bug 14122: Hide logo if TOR\_HIDE\_BROWSER\_LOGO set
        -   Translation updates
    -   Bug 13379: Sign our MAR files
    -   Bug 13788: Fix broken meek in 4.5-alpha series
    -   Bug 13439: No canvas prompt for content callers

