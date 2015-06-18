---
layout: post
title:  "How to setup swap on Amazon AWS EC2 easy and the right way without tricks"
date:   2015-06-18 10:00:00
categories: aws ec2 linux
---

I found a lot of articles and topics on this question, but none were like how I want to show you to create like on a normal Linux machine the necessary swap you need.

On a normal Linux machine you would have a dedicated **swap** partition.

Relying on a swap file anywhere on your normal partitions it's not really recommended, it's just a desperate solution.

## We want 100% to use the resources for getting the top performance.

So, in your AWS Console, edit create an EBS Volume, the size that you need, usually a 2GB will fit any need, or less for smaller machines and select like the last availeble /dev entry, for example /dev/sdm. Use the normal SSD one and not magnetic, as if your server will start using the swap, you will regret if you choosed Magnetic.

Now edit your machine and attach the fresh created block device to it.

Log into your machine, become root and run the following:

```
mkswap -L SWAP /dev/xvdm
```

Edit /etc/fstab and add next entry as the last line if possible:

```
LABEL=SWAP  none    swap    defaults    0 0
```

Now, important, reboot. Doing swapon the fresh swap device will not work on most instances created, maybe that's the reason the others do the tricky file variant.

Relogin, test (free -m) and enjoy.