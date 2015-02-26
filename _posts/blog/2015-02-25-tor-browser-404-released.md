---
layout: post
title: "Tor Browser 4.0.4 is released"
permalink: tor-browser-404-released
date: 2015-02-25 21:12:56
author: mikeperry
category: blog
comments: open
tags: ["tbb", "tbb-4.0", "tor browser", "tor browser bundle"]
---

A new release for the stable Tor Browser is available from the [Tor Browser Project page](https://www.torproject.org/download/download-easy.html) and also from our [distribution directory](https://www.torproject.org/dist/torbrowser/4.0.4/).

**Note:** The individual bundles of the stable series are signed by one of the subkeys of the Tor Browser Developers signing key from now on, too. You can find its fingerprint on the [Signing Keys](https://www.torproject.org/docs/signing-keys.html.en) page. It is:

    pub   4096R/0x4E2C6E8793298290 2014-12-15
          Key fingerprint = EF6E 286D DA85 EA2A 4BA7
                            DE68 4E2C 6E87 9329 8290

  
Tor Browser 4.0.4 is based on Firefox ESR 31.5.0, which features [important security updates](https://www.mozilla.org/security/known-vulnerabilities/firefoxESR.html#firefoxesr31.5) to Firefox. Additionally, it contains updates to NoScript, HTTPS-Everywhere, and OpenSSL (none of the OpenSSL advisories since OpenSSL 1.0.1i have affected Tor, but we decided to update to the latest 1.0.1 release anyway).

Here is the changelog since 4.0.3:

-   All Platforms
    -   Update Firefox to 31.5.0esr
    -   Update OpenSSL to 1.0.1l
    -   Update NoScript to 2.6.9.15
    -   Update HTTPS-Everywhere to 4.0.3
    -   Bug 14203: Prevent meek from displaying an extra update notification
    -   Bug 14849: Remove new NoScript menu option to make permissions permanent
    -   Bug 14851: Set NoScript pref to disable permanent permissions

