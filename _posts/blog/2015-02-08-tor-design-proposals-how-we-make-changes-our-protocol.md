---
layout: post
title: "Tor design proposals: how we make changes to our protocol"
permalink: tor-design-proposals-how-we-make-changes-our-protocol
date: 2015-02-08 01:22:58
author: nickm
category: blog
comments: open
---

(This post is likely to be interesting for folks who want to know how the Tor software is made.)

At the core of the Tor software lies the network protocol that Tor relays and clients use to talk to each other. We try to make sure we have a [good set of specification documents](https://gitweb.torproject.org/torspec.git/tree/) for the protocol at all times, so that other people can write compatible software that interoperates with Tor.

Once upon a time, we used to change these specification documents whenever we changed the software's behavior. That didn't go well. We would have changes in the spec that we had forgotten to make in the software, and tons of inline comments where we argued about whether a particular paragraph was a good idea.

So back in 2007, we introduced a lightweight change-proposal process: to make a change to the Tor protocol, you write up a little design document, and send it to the tor-dev mailing list. Once it meets editorial quality, it can go into the [proposals repository](https://gitweb.torproject.org/torspec.git/tree/proposals). Once it's implemented, it can be merged into the spec.

There are a lot of proposals to look at, though. The current set of open proposals has almost 100,000 words in it! (That's almost half again as long as the Tor specs themselves.)

To help people navigate through this pile of design proposals, I started to write a regular "proposal status" email to explain what all of the open proposals are about. Last year, however, I fell out of the habit. Tonight, I've tried to fall back in: [here's the latest proposal status writeup](https://gitweb.torproject.org/torspec.git/tree/proposals/proposal-status.txt).

Below the cut, my summaries of the still-open proposals that have been added in the past couple of year -- and thanks to all the busy designers who have been working to think of ways to improve Tor!

<!-- more -->

228 Cross-certifying identity keys with onion keys

This proposal signs each server's identity key with its onion  
 keys, to prove onion key ownership in the router descriptor.  
 It's not clear that this actually improves security, but it  
 fixes an annoying gap in our key authentication. I have it coded  
 up in my \#12498 branch, targeting 0.2.7. (2/2015)

229 Further SOCKS5 extensions

Here's a nice idea for how we can support a new SOCKS5 protocol  
 extension to relay information between clients and Tor, and  
 between Tor and pluggable transports, more effectively. It  
 also adds some additional SOCKS5 error codes. There are some  
 open questions to answer. "Trunnel" has an implementation of  
 the protocol extension formats in its examples directory. (2/2015)

230 How to change RSA1024 relay identity keys [DRAFT]  
 231 Migrating authority RSA1024 identity keys [DRAFT]

Who remembers the OpenSSL "Heartbleed" vulnerability?  
 These proposals I wrote try to explain safer mechanisms for a bunch  
 of servers to migrate their RSA1024 identity keys at once. I'm not  
 sure we'll be able to build thee, though: implementating proposal  
 220 above seems cleverer to me. (2/2015)

232 Pluggable Transport through SOCKS proxy [OPEN]

Arturo Filastò wrote this proposal for chaining pluggable  
 transports which themselves need to go through proxies. Seems  
 potentially useful! (2/2015)

233 Making Tor2Web mode faster [OPEN]

This one by Virgil, Fabio, and Giovanni describes a couple of ways  
 that Tor2Web builds of Tor can save some circuit hops that they use  
 today. Potentially useful for Tor2Web; any implementation needs to  
 be sure that it never changes the behavior of non-tor2web clients.  
 (2/2015)

234 Adding remittance field to directory specification [OPEN]

Virgil, Leif, and Rob added this proposal for relays to specify  
 payment addresses for schemes that want to compensate relay  
 operators for their use of bandwidth. (2/2015)

235 Stop assigning (and eventually supporting) the Named flag [DRAFT]

This proposal is about removing the Named flag. (Thanks to  
 Sebastian Hahn for writing it!) The rationale is that the naming  
 system for relays never worked particularly well, and it had  
 strange and hard-to-explain security properties. We've implemented  
 the key part of this already: directory authorities don't assign  
 the Named flag any longer. Next up will be removing client support  
 for parsing and understanding it. (2/2015)

236 The move to a single guard node [OPEN]

This proposal suggests that to limit client fingerprinting, and to  
 limit opportunities for attacks, clients should use a single guard  
 node, rotated infrequently. This transition is in progress; we use  
 a single guard node for circuit traffic now, but in order to make  
 guards more long-lived, we need to adjust how they are chosen.  
 George has a patch for that as \#9321, targetting inclusion into  
 0.2.6. (Thanks to George Kadianakis and Nicholas Hopper for  
 writing this one.) (2/2015)

237 All relays are directory servers [OPEN]

Matthew Finkel wrote this proposal to describe a transition to a  
 world where Tor relays can be directory servers without having an  
 open DirPort -- and eventually, where every relay can be a  
 DirServer. He has an implementation, possibly for 0.2.6 or 0.2.7,  
 in ticket \#12538. (2/2015)

238 Better hidden service stats from Tor relays [DRAFT]

Here's an important one that needs many eyes. George Kadianakis,  
 David Goulet, Karsten Loesing, and Aaron Johnson wrote this to  
 describe a mechanism for the tor network to securely produce  
 aggregate hidden service usage statistics without exposing  
 sensitive intermediate results. This has an implementation in  
 0.2.6 and should probably be marked closed. (2/2015)

239 Consensus Hash Chaining [DRAFT]

Here's the start of a good idea that Andrea Shepard wrote up (with  
 some help from Nick). The idea is to make it hard even for a set  
 of corrupt authorities (or authority-key-thieves) to make a  
 personalized false consensus for a target user, by authenticating  
 the whole sequence as a hash chain. Others on tor-dev suggested  
 improvements and had good questions (thanks, Leif and Sebastian G!)  
 (2/2015)

240 Early signing key revocation for directory authorities [DRAFT]

This one is another Andrea+Nick collaboration about certificate  
 revocation for our most sensitive keys. If an authority key needs  
 to be replaced, it would be great to take the old one out of  
 circulation as fast as possible. Peter Palfrader on tor-dev had  
 some ideas for making this better. (2/2015)

241 Resisting guard-turnover attacks [DRAFT]

I wrote this one with good ideas from Aaron Johnson and Rob  
 Jansen. It describes a way to respond to an important class of  
 attacks where an adversary kills off a targeted user's guards until  
 the user has chosen a guard the attacker controls. (See the  
 "Sniper Attack") paper. The defense is tricky, and if not done  
 right, might lead clients to kick themselves off the network out of  
 paranoia. So, this proposal could use more analysis. (2/2015)
