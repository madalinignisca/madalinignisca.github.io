---
title: OpenEBS on MicroK8S on Hetzner
type: post
date: 2022-09-06 17:30
categories: wpk8s,openebs,microk8s,hetzner,cstor,jiva
---

Last few months I experimented more and more with all OpenEBS solutions that fit small Kubernetes cluster, using MicroK8S and Hetzner for a real experience.

Initially I thought that Jiva is the best choice, as this backend is easy to maintain and ignoring Cstor as long time maintanance seemed to be too complex for less experienced people.

So my discoverings made me realise that both Cstor and Jiva have their good cases and a decision which one to use from my point of view is simple:

If you want only a small minimum 3 nodes cluster, with expected storage requirements, possible with no expansion in the future, Jiva is the main choice, as on future upgrades, any manual steps will not be needed.

Jiva Storage Classes are defined to use for the storage replicas other dynamic storage classes (defined in Jiva Policies), and stright forward is to use OpenEBS localpath.

On Hetzner on most cases I add each of the 3 nodes an expected block volume with estimated initial size and create the Normal Storage Class. I create also a Fast Storage Class that uses the nodes local storage, which Hetzner provides local NVMe drives with best possible IOPS in all the public cloud industry. Anyway, the attached block storage have higher IOPS than premium storage on any other public cloud, and can be used for almost all cases also.

The idea with attached volumes on Hetzner is that you can increase size on the fly. I manage myself the initial formating with EXT4 and resize in realtime is easy using parted and resize2fs. Usually I use Ansible and run this in parallel on all 3 nodes, but if you are going to try, do it manually a few times than automate, to be fully confident in what you learn.

For the future, as I do Helm updates to the OpenEBS deployment, with Jiva I don't have any changes to do, volumes being on localpaths in reality, files are natively written to EXT4 file system, it is the easyest mode possible from my point of view.

Now on Cstor, which on my first attemps, looked more complicated, and I could not find a real business case to use it, as Jiva is fitting my clients and projects almost in all cases. But one day after re-reading the Cstor documentation again and again, **I saw it**. I can have POOLS of attached block volumes and the out of the box setup of Cstore with OpenEBS Node Disk Manager made me realise that Cstor is the best choice for a project I started recently, and to which sold storage for applications is a promise to the consumer that is THICK allocated to them, and I don't do oversell (Jiva with localpath would be that by default as it allows overprovisioning by default).

Both Cstor and Jiva can allow over provisioning or not, depedning on how you tweak it, but in my business case, Cstor would provide "block storage" to Deployments or Stateful Apps that the "disks" can be formated with needed filesystems (some require XFS, some EXT4, some clients kindly asked to have it BTRFS). As choice of filesystem did not bother me, I ended up implementing Cstor as this made clients happy (you do look better when you are flexible and provide the features clients demand, if that doesn't complicates your work).

The last experiment went with the recent Mayastor engine, which I still want to experiment more, but the first real blocker to use it, is that it's minimal requirements only to run are very high, and in most projects using MicroK8S to deploy a Highly Available ecommerce shop for example, to have Mayastor already increases the hardware requirements visible in public cloud costs (yes, for many clients even 100 euros extra per month must be really well justified). As initial benchmarks on how Woocommerce or Magento runs in a MicroK8S environment on Hetzner, I did not see a viable justification for using Mayastor, as with minimal caching done well on both WordPress and Magento side, both load tests provided same results. In both cases, MySQL was deployed using Percona Operator which uses hostpath, so DB access speed was at native NVMe speed of the local disks, and assets were cached by Nginx with cache path set to also a temporary localpath mount. Keeping all uploaded images of products on Mayastor provided zero advantange, simply increased the price for larger cloud servers.

My conclusion is use Jiva for most cases, Cstor when you want to expand by adding disk nodes. Avoid Mayastor if you are not in the high pay niche.

If you want to find out how I do all the stuff described above, don't hesitate to buy my book [**WordPress on MicroK8s**](https://leanpub.com/wp-microk8s/overview). At this moment I'm finishing the chapter on storage and soon to publish a new update describe both using Jiva and Cstor on MicroK8S in Hetzner cloud.
