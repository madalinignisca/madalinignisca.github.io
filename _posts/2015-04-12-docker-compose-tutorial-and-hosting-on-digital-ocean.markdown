---
layout: post
title:  "Docker Compose Tutorial and hosting on Digital Ocean"
date:   2015-04-12 07:09:43
categories: docker compose tutorial hosting digitalocean
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

// <mark>TOBEDONE</mark>

### Linux (Ubuntu/Debian) setup

// <mark>TOBEDONE</mark>

### Linux (Fedora/Centos/RHEL) setup

// <mark>TOBEDONE</mark>

.....

## REMOTE Setup (Digital Ocean one thing to do)

On [Digital Ocean](http://goo.gl/idAtX4) after we have setup an account (you must have at least a first time payment of $5 to use their services), we need to create a special secret HASH key to use it with Docker Machine to access their API, as this will provide control to any of the instances hosted in that account. The key must be copied as you can't retrieve it anymore after.

Once the key is generated, **make sure** that you will save it to a private note that you can access anytime you will need it. I use for example [Keep](http://keep.google.com/) from Google.

## Create a "recipe" for your project

Hosting with Docker gives us the possibility to separate services and scale to multiple instances very easy.

To do this, I love the Docker Compose, previously know as Fig, a tool that comes with Docker and helps maintaining multiple instances related to the project you work on.

Every command will be run from the Git Bash terminal

### How do I prepare my projects:

I keep my projects in one folder, under my user account: "C:\\Users\\\<gabb3\>\\Workspace\\projects".

For our tutorial, I'll create a few demo sites using WordPress, Concrete5, Joomla, Drupal and Magento, so you will really see the simplicity of hosting PHP applications and be able to scale them very easy when a website would require more power to handle a bigger spike in traffic.

### WordPress Docker recipe:

In your projects folder create a new directory named as you wish. Here we will call it "WordPress".

``` bash
cd /c/Users/<gabb3>/Workspace/projects/
mkdir -p WordPress
```

Now open this folder with your favorite Code Editor (I recommend [Atom](http://atom.io/) in case that you still research for a good quality code editor).

We need to create first a "Dockerfile" that will be used to build the main web server. To keep it simple for WordPress, we will use the official [WordPress](https://registry.hub.docker.com/_/wordpress/) with Apache. Put the following code in the file:

``` Yaml
FROM wordpress:4.2.1-apache

RUN echo "upload_max_filesize = 16M" > /usr/local/etc/php/conf.d/custom.ini \
    && echo "post_max_size = 16M" >> /usr/local/etc/php/conf.d/custom.ini \
    && a2enmod expires headers rewrite
```

Line 1 is telling Docker that we want to build a custom image from WordPress
Lines 3 to 4 are creating a custom ini file for php that will set the max upload size to 16MB. Adjust to your needs.
Line 5 will enable in Apache 3 modules necessary for Pretty urls and expiration of served files as we will want it.

Great! Now let's create the Compose file that will be used to create and handle our instances. Create a new file named "docker-compose.yml".

``` Yaml
db:
  image: mariadb:10.0.17
  environment:
    - MYSQL_ROOT_PASSWORD=<root_password>
    - MYSQL_USER=<db_user>
    - MYSQL_PASSWORD=<db_password>
    - MYSQL_DATABASE=<db_database>
  cpu_shares: 77
  mem_limit: 144m

www:
  build: .
  ports:
    - "10080:80"
  links:
    - db:mysql
  cpu_shares: 160
  mem_limit: 320m
```

This config is optimized for a production setup that is very safe. Now let me explain each line and what changes you should make per your needs.

**"db"**:

* we use the image **mariadb** and set an exact version as we want to manually test when we really need to upgrade it. As long as there are no security mandatory updates, you are safe to stay with the version you choose at the start of a project. **Upgrades must be always tested!**
* **environment**: all are required to initialize the database. Change what's in \<...\> with your own wish. I personally use random generated strings here with only small letters and numbers. Ugh, I'm a security freak.
* **cpu_shares**: this will tell Docker how much of the CPU to use. The value can be from 1 to 1024 where 1024 is 100% of it.
* **mem_limit**: the maximum amount of ram to be used by the instance. I'm setting this two values as I want 100% control on the host's resources in case that a website goes mad from many reasons and the others are not affected at all.

**"www"**:

* **build**: simple, build from the Dockerfile that we prepared in the root of the project.
* **hostname** and **domainname**: are used to set the instance proper hostname. Change as needed to your website.
* **volumes_from** will attach our common file system for WordPress uploads.
* **ports** will expose our web server to the master host so the website can be accessed.
* **links** is setting a network communication channel to the database and let's our webserver find the database on the host "mysql". This way we don't care about it's IP which can change.

As you can see I've set certain values to the CPU and RAM usage to be safe and you can adjust them as required. This depends a lot on how many plugins you add and how your WordPress theme is done. This values are very safe for a basic setup and using a few plugins I prefer like Jetpack, WordPress SEO, Google Analytics for WordPress and even BuddyPress with bbPress. For better performance instead of increasing this values, a cache instance with Memcached would be preferred as it would provide better speed and use less CPU and RAM.

Now it's time to test our recipe and if all goes OK, we can provision it to [Digital Ocean](http://goo.gl/idAtX4) later.

As we haven't done anything to docker to communicate with the remote machine that we haven't started yet, we will test it on our local workstation first.

In GIT BASH run:

``` bash
$ boot2docker init
$ docker-compose up
```

Line 1 is to initialize the Docker virtual machine for the first time. This is done once and we don't need it anymore after. Alternative we could use docker-machine but it goes beyond the scope of this first tutorial.
Line 2 will start preparing the containers for the first time and start them if all goes ok.

To access the website we need to know on what ip and port it runs.
Run:
``` bash
$ boot2docker ip
```
in the GIT BASH. The port we already know as we hardcoded it in the <mark>docker-compose.yml</mark> file.

```
http://192.168.59.103:10080/
```

Go on and install WordPress and continue to play.

Now we will continue with another CMS, [**Concrete5**](http://www.concrete5.org/).

### Concrete5 Docker recipe:

// <mark>TOBECONTINUED</mark>

// <mark>TODO</mark> make annotated screenshots using Skitch

## Version history

* 2015-05-03
  Updated WordPress recipe, using WordPress 4.2.1
