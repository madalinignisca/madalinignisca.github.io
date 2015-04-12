---
layout: post
title:  "Host your websites with Docker on Digital Ocean"
date:   2015-04-12 07:09:43
categories: docker digitalocean
---

> Hosting with Docker on [Digital Ocean](http://goo.gl/idAtX4)
> is really simple!!!

Hello visitor!

I bet you got here searching a more complete tutorial on how to host websites using Docker and a good quality cloud hosing provider.

While there are lots of cloud hosting providers, I recommend for small startups to use [Digital Ocean](http://goo.gl/idAtX4). Use my link to get an extra $10 credit if you don't have yet an account.

The virtual machine (droplet) size depends on your applications requirements, for example for a WordPress website you should start with one using 1GB of ram at least. It is really necessary to have at least an amount of ram available for the mandatory processes that Docker needs (Linux services included), as I would estimate at least 512MB to be safe. The rest would be required on the applications needs.

Also, like on almost all providers, the CPU is the logical one and not the real hardware core.

## Local setup

To start we need on our local machine all the tools necessary to manage Docker both local and remote.

From the first day I started with Docker, all things I've learned where from the official website, and I agree that the documentation is not very friendly to beginners in Unix stuff. To handle things, you need to have at least some basic knowledge on how each service you require can be configured.

But for what I intend to present in this tutorial, you should at least know how to use a computer to input some commands in the command line (CMD on Windows, Terminal on Mac, Linux users should know more already).

I presume that you are not using already any virtualization solution on your workstation/laptop as a certain solution will be used here.

### Windows setup

First let's download the mandatory stuff that we will setup on our workstation:

* [GIT](http://git-scm.com/download/win)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Docker](https://github.com/boot2docker/windows-installer/releases/latest)
* [Docker Machine](https://docs.docker.com/machine/)

I recommend to install them separate even if Docker comes as an All In One package, but as a web developer you should control your software and customize the way you need your installations.

One optional thing, but that would make sure that certain issues will never be encountered is to install anything without using spaces in the PATH to any executable or library of any tool you use.

For example I use a base PATH for my tools in "C:\\tools". Git would be installed in "C:\\tools\\git", VirtualBox in "C:\\tools\\virtualbox", Docker in "C:\\tools\\docker" and so on for many others (ruby, python, php, etc.).

Docker Machine is a simple executable that you should place it in the Docker's bin folder in it's installation PATH. Maybe someday they will include it in the Docker installation package.

Now that you have installed all necessary tools, let's prepare a ssh key that you will need on different things and of course necessary to keep safe your projects if you haven't done it until now by using GIT.

Start **GIT Bash** and let's input some commands. Replace what you see here in \<...\> with what suits you. For example \<dag33k@gabe.me.uk\> is my email and you should replace it with yours. Also don't put the \<...\>.

``` bash
$ ssh-keygen -C <dag33k@gabe.me.uk>
```

This will generate our private and public keys, used to communicate by SSH and other tools that can communicate over SSL.

You should make a copy of he generated files and keep them private! The files can be located in "C:\\Users\\\<your_user\>\\.ssh". The "id_rsa" file without an extension is the private key. **This file you never give it or it's contents to anybody ever!!!**

The content from "id_rsa.pub" is to be used for many web services like Github, Gitlab, Bitbucket or login without password in ssh/sft servers.

### Mac OS X setup

@TOBEDONE

### Linux (Ubuntu/Debian) setup

@TOBEDONE

### Linux (Fedora/Centos/RHEL) setup

@TOBEDONE

.....

## REMOTE Setup (Digital Ocean one thing to do)

On [Digital Ocean](http://goo.gl/idAtX4) after we have setup an account (you must have at least a first time payment of $5 to use their services), we need to create a special secret HASH key to use it with Docker Machine to access their API, as this will provide control to any of the instances hosted in that account.

Once the key is generated, **make sure** that you will save it to a private note that you can access anytime you will need it. I use for example [Keep](http://keep.google.com/) from Google.

@TOBECONTINUED

@TODO make annotated screenshots using Skitch
