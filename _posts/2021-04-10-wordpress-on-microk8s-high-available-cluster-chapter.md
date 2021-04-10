---
title: High Available cluster chapter in WordPress on MicroK8s book
type: post
date: 2021-04-10 08:30
categories: wpk8s
---

Finally I reorganized my personal free time, with a side project in progress, and now I'm continuing working on my [WordPress on MicroK8s](https://leanpub.com/wp-microk8s)
again.

New chapter on High Availability setup is almost completed by this morning, and following a new publish update to do as will finish it by next week.

This chapter was delayed as OpenEBS was part of a Pull Request to join next stable version of MicroK8s, and it allows us users of MicroK8s to simply enable it
and not care anymore about us maintaining it. Thank you Canonical for that, and I do hope to see them adding **cert-manager** as well :)

This new chapter brings you the most basic knowledge to construct your cluster with ready to use high available storage, improve the WordPress recipe to allow
self-healing when a node becomes unavaialble, we even simulate this to learn the process, and allowing multiple replicas of WordPress to run, so we can benefit
of better performance when traffic is high, and scale down when traffic becomes low, allowing saving of money without downtime also.

With this, I now going to continue the work on the book every weekend until will be fully finished, publishing an update of the book as each new chapter is completed.
