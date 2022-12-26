---
title: 'How to: permanent private ip on Multipass on Windows with Hyper-V'
date: 2022-09-07 7:30
tags: multipass microk8s windows hyperv ubuntu kubernetes
category: devops
layout: post
---

If you use [Multipass](https://multipass.run) on Windows with Hyper-V, when running MicroK8S or possible other services, you will notice that on restart of the instance or of the host, MicroK8S will not work for you.

The issue is that the assignated IP by the default V-switch of Hyper-V that provides also internet connectivity to your instances will always assign a different ip address to the instance.

Services like Kubernetes, MicroK8S, K3S, expect that the main IP used will not change. Working with changing IP addresses is more complex, but doable.

For Hyper-V on Windows, there is an easy to use solution: add a secondary V-Swith of type internal. Private can be used, but there will be some additional complexity unnecesarry for using Multipass and MicroK8S.

So open Hyper-V manager and in the V-Swith section add a new switch called for example `multipass`. Keep the name simple, one word and lower case. If not, you will understand yourself later why I advise so.

Now, when you want to start a new Multipass instance, add the network param. Example:

`multipass launch -n microk8s-3 -c 2 -m 4G -d 40G --network name=multipass,mode=manual`

This will give us in the instance a secondary ETH1 network interface that waits for us to configure it.

Do not try to find a way to do dhcpd with the new v-switch, as 99% of cases you will have identical same situation like with main default V-Switch, random ip addresses.

Now, shell in the instance and add a prepare netplan file:

`ip l` --- note the MAC address of ETH1 (I copy it in notepad, to be able to copy paste it later)

`sudo nano /etc/netplan/99-multipass.yaml`

Paste the following template and change the MAC and the IP address including netmask to fit your requirements.

```
network:
    ethernets:
        eth1:
            dhcp4: false
            match:
                macaddress: 52:54:00:d4:44:41
            set-name: eth1
            addresses: [10.0.1.1/16]
    version: 2
```

The only important thing is that your machines use identical netmask, so the ip class is not important if it is different from groups of instances to others, as the added vswith is like a dump simple hardware network switch in this case.

I used 10.0.0.0/16 for the instances, as for some experiments with no tunnel networks for pods Microk8s does 10.1.0.0/16 and I am matching this setup in Hetzner with their private network and automatic routes creation using the hetzner ccm for kubernetes (this is another topic, but for me this way of using Hyper-V allowed me to replicate the Hetzner Cloud locally and experiment without expenses).
Any other projects outside of MicroK8S, I use other ip address classes.

Run:
`sudo netplan apply`

This will freeze the CLI. If u leave it like this a couple of minutes it will return to your CMD prompt, or if u are impatient, close current windows terminal tab, open another one and shell in the instance again. Test now with :
ip a and you should see ETH1 configured.

Enjoy!

