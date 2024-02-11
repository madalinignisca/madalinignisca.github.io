---
title: High Available Cluster for WordPress on MicroK8s
layout: post
date: 2022-05-04 18:30
categories: wpk8s
---

Been a long time, passed through some things, including Covid, but now back on track, back on the book.

Been refreshing all chapters up to the one on High Availability. The new edition of the book, that anyone
that bought the book will be able to download in their account for free, will change the OpenEbs CSI driver
to [https://longhorn.io/](Longhorn).

After many months of using both, I came to the conclusion that Longhorn, although it's not modular as OpenEBS,
it is a much more simple solution with extra nice features for people that are not experts in Kubernetes.

Longhorn has a more simple install procedure, offers also a more simple aproach to allow a volume to be accessed by many pods.

Although I did not benchmark myself, Longhorn is praised for being faster than OpenEBS Jiva, the simple option for replicated volumes with OpenEBS.
Another point is Longhorn including the NFS builtin support uses almost half the ram then OpenEBS Jiva + NFS provisioner.

Other advantages for Longhorn, which I will present in later chapter dedicated to backups, is that Longhorn provides an admin UI and also
support to do backups to S3 compatible services.

As I don't want to enforce WordPress users to change their normal way of using the uploads, when we want to scale our
WordPress service to many instances, the volume on generic CSI drivers can't be used from many replicas. Longhorn, like OpenEBS, but
more easy, allows to simply declare the volume access mode to ReadWriteMany and WordPress can be scalled to as many replicas
our budget can afford.

Also, Longhorn is doing volume replication almost in real time, so our MySQL and WordPress attached volumes will not vanish easy in case
that a node would even be destroyed.

So, with refactoring and completing this chapter, I will push an update to the book which makes it almost complete for anyone that would
stick to a more WordPress way of managing the application, meaning that with this finished setup, on a cluster of minimal 3 MicroK8s nodes,
will benefit of high availabilty, easy self healing of cluster options, easy handling backups and continuing to handle WordPress
exactly like before, meaning including adding/deleting plugins and themes, also updates can still be done from the WordPress dashboard.

Using more modern ways to put WordPress, with source code under version control, it is a topic outside of the purpose of the book, and for sure
people already working with WordPress that way, can easily know how to construct a container out of it and replace the WordPress official container
image with their own image. The only thing is to point the shared volume to `/wp-content/uploads` and create any extra cache or temporary volumes using
*emptyDir* volumes.

Only some final touches and hope that by this weekend I'll make the update available on [https://leanpub.com/wp-microk8s](Leanpub).
