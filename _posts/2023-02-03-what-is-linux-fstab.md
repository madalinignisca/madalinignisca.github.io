---
title: 'Linux Fstab Explained'
layout: post
date: 2023-02-03 19:30
tags: linux filesystem fstab
category: linux
image: https://source.unsplash.com/NLSXFjl_nhc
---

Linux fstab, also known as the file system table, is a configuration file located in the /etc directory. It contains information about the various file systems that are used by Linux and how they are to be mounted. This includes information about the type of file system, the mount point, the options to be used when mounting, and the dump frequency.

![Linux terminal with distribution information from neofetch](https://source.unsplash.com/NLSXFjl_nhc)

The fstab file is used to specify the type of mount that should be done. This can include local file systems, network file systems like NFS and Samba mounts, and CD-ROMs. It is important to note that the order of entries in the fstab file is important. Entries that have higher priority will be mounted before entries with lower priority.

When a system boots up, the fstab file is used to mount the various file systems. This is done by running the mount command with the -a flag, which tells the mount command to mount all the file systems listed in the fstab file. After the file systems are successfully mounted, the system can then be used as usual.

Let’s look at a few examples of entries in the fstab file. An NFS mount might look something like this:

`/mount/server1:/share /mnt/server1 nfs defaults 0 0`

This tells the mount command that the remote file system /share on server1 should be mounted to the local directory /mnt/server1. The defaults option tells the mount command to use the default options for mounting. The 0 0 at the end tells the dump and fsck commands not to check the file system.

A Samba mount might look something like this:

`//server2/share /mnt/server2 cifs credentials=/etc/samba/creds 0 0`

This tells the mount command that the remote file system /share on server2 should be mounted to the local directory /mnt/server2. The cifs option tells the mount command to use the CIFS protocol for mounting. The credentials option tells the mount command to use the specified credentials file for authentication. The 0 0 at the end tells the dump and fsck commands not to check the file system.

In summary, the Linux fstab file is a configuration file located in the /etc directory. It contains information about the various file systems that are used by Linux and how they are to be mounted. This includes information about the type of file system, the mount point, the options to be used when mounting, and the dump frequency. When the system boots up, the mount command is run with the -a flag to mount all the file systems listed in the fstab file. Examples of NFS and Samba mounts are included in this article.
