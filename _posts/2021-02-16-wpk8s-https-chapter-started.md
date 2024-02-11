---
title: Started HTTPS chapter in WordPress on MicroK8s
layout: post
date: 2021-02-16 07:00
categories: wpk8s
---

Spent one hour today, like I intend for most of the mornings to do when
I work on the **[WordPress on MicroK8s](https://bit.ly/wpk8s-leanpub)** book
writing the introduction on securing with certificates a WordPress website
on Kubernetes.

As the book is with opinionated solutions I use, the first part of the chapter
focuses on setting up Cloudflare, to benefit of their easy and automated
certificates management, for free, and extra protection to the server,
by allowing communication strictly between Cloudflare and the service. This way,
a website is not only serving visitors by https, but it is also protected
additionally from DDOS attacks, adds caching of any well setup cashable response,
and blocks most of offending traffic. It allows to block all traffic that is
not coming from Cloudflare directly to the server, even more, the server's ip
could be even never discovered by attacker, so they would not be even capable
to try alternatives, like trying to exploit an unmaintained old version of ssh,
or forgotten not well secured ftp or rpc service exposed to the internet.

This week will be focused on writing the full scenario on with Cloudflare, followed
next week by a Let's Encrypt certificate implementation with automation to renew it.
The readers should pick their preference on which scenario they find best.
