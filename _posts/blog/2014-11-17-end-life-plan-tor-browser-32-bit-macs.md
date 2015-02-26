---
layout: post
title: "End of life plan for Tor Browser on 32 bit Macs"
permalink: end-life-plan-tor-browser-32-bit-macs
date: 2014-11-17 19:18:41
author: mikeperry
category: blog
comments: closed
---

We are planning to discontinue support for 32 bit Macs for Tor Browser.

We're doing this for two main reasons. First, Apple itself no longer supports 32 bit Macs. The only remaining 32 bit Mac users are on OSX 10.6, which Apple ended support for in [February of this year](http://arstechnica.com/apple/2014/03/snow-leopard-updates-are-probably-done-here-are-your-os-x-upgrade-options/). Second, 64 bit software has improved security properties by way of improved address space layout randomization (ASLR), which makes exploitation more difficult.

This transition will happen in phases: First, the upcoming 4.5-alpha series will only be available as 64 bit builds. We will continue releasing 32 bit versions of the 4.0 series until the 4.5 series is declared stable. When the 4.5 release stabilizes, all support for 32 bit Macs will end. The 4.5 release series will be stable "when it's ready", but we know we need to perform at least two more releases in this series to properly exercise the new security features in the updater. This means that 32 bit Mac users likely have a month or two to decide what to do.

Current 32 bit Mac users have a few options. If your actual Mac hardware is 64 bit capable, you can upgrade to either the 64 bit edition of OSX 10.6 (which we will continue to support for a bit longer), or use the app store to upgrade to 10.9 or 10.10.

If your hardware is not 64 bit capable and won't run these newer Mac operating systems, you should still be able to use [Tails](https://tails.boum.org/download/index.en.html), which contains the Tor Browser. You can run Tails in a virtual machine such as [VirtualBox](https://www.virtualbox.org/), or you can [manually install it to a USB disk from the Mac OS Terminal](https://tails.boum.org/doc/first_steps/installation/manual/mac/index.en.html). If you install Tails to a USB stick, you will need to [reboot your Mac](https://tails.boum.org/doc/first_steps/start_tails/index.en.html#index2h2) in order to use it.

  

All Mac Users: Manual Update Required
=====================================

The transition from 32 bit Mac bundles to 64 bit Mac bundles means that our (currently experimental) in-browser updater will not transition any Mac users to the 64bit version automatically, even if your Mac is already running a 64 bit version of Mac OS. You must perform this update manually, as you had to do prior to the 4.0 series. This means downloading [the DMG](https://www.torproject.org/download/download-easy.html#mac) and dragging the new 64 bit Tor Browser over your old Tor Browser, and replacing the application.

Once you are running the 64 bit version, updates should function correctly again.
