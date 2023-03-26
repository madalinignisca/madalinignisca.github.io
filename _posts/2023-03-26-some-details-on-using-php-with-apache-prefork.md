---
title: 'How to configure Apache MPM Prefork with mod_php for performance and stability'
type: post
date: 2023-03-26 08:00
tags: php apache prefork mod_php oom
category: devops
image: https://source.unsplash.com/-6SmukZ_w6s
---

Why you should never use Apache with mod_php in the frontend? Because PHP can take your services to Out Of Memory when somebody really wants to take your website down. Read next about this.

![Elephants family](https://source.unsplash.com/-6SmukZ_w6s)

First, I am not against Prefork. I find it actually a decent way of running PHP, but only if it is for handling PHP and no static files. When it is used in combination with another web server (Apache included) and proxying to it only PHP requests, can help to make the usage of many popular web applications even easier, as for example WordPress with some plugins will always set extra directives in .htaccess (consider W3 Total Cache for example).

But read the following to understand what you are facing leaving it with defaults and allowing it to be hit directly from the Web.

Next are the default values of how Prefork will be configured.

StartServers 5<br/>
Number of child server processes created at startup

MinSpareServers 5<br/>
Minimum number of idle child server processes<br/>
If only <= 5 concurent requests happen, max 5 processes will live, but if serving static files, you'll see this up after just a few minutes, hours.

MaxSpareServers 100<br/>
Maximum number of idle child server processes<br/>
If you are trying to set the value equal to or lower than MinSpareServers, Apache HTTP Server will automatically adjust it to MinSpareServers + 1.<br/>
As concurent requests happen, this will become current idle number of processes, and all above 100 idling will be terminated. Why waste cpu time on handling this? I would set it to MaxRequestWorkers value.

MaxRequestWorkers 256<br/>
Maximum number of connections that will be processed simultaneously<br/>
Put this on a heavy Magento website and cry if you don’t have  64GB of RAM only for Apache + mod_php 😂

ListenBacklog 511<br/>
Maximum length of the queue of pending connections<br/>
Will be useful for queuing more requests if your requests finish really fast (<50ms), but consider going horizontal scalling if you do more than 2-4 concurent requests per real cpu core.

ServerLimit 256<br/>
Upper limit on configurable number of processes<br/>
Use this directive only if you need to set MaxRequestWorkers higher than 256 (default). Do not set the value of this directive any higher than what you might want to set MaxRequestWorkers to.<br/>
Human explanation: DON’T YOU EVER F\*\*KING THINK TO SET THIS VALUE VERY HIGH!

What it means is if you are hit on 256 HTTP requests in PHP, you will have 256 processes trying to concurrently do work.

If you are on a BIG server, saying you have 32, 64 real cores, that means no VCPU as that is already 1 core with 2 threads fighting for resources, it might play nice, as long as you have the amount of RAM that your php request will need to be handled.

For example, if you have a Symfony app that on each request uses in average 40mb of ram, to be safe, you should have your server with 10 GB of ram only for Apache + PHP and some extra for the OS to behave, so actually over 12 is safe. This is considering that the server will do only Apache + mod_php and not extra databases or others.

If Apache + mod_php is a must, you should calculate your MaxRequestWorkers to the max it can be handled.

You must benchmark your application for memory usage first. Speed is not the main issue here, as you must calculate how much RAM will be used on max concurent requests.

From personal observation, for common popular PHP apps, I observed that WordPress for example averages around 40MB, when using just few plugins (contact form 7 with an extra storage plugin) and a theme like Divi.

I tweaked many WordPress websites to ditch plugins and move in the theme a lot of extras, like meta directives in the header, Google Analytics etc. directly as html/js/css things as necessary. This always helped getting rid of about 10MB in total from all the extra plugins per each request.

If you use WooCommerce, you should raise your expectations to 60MB if you avoid any useless plugin (again, try to build in theme templates all you really need, avoiding PHP as much as possible).

On an plugins abusive WordPress website, think towards 90-120MB per request and accept high costs for hosting it.

Don’t forget that the the Admin of WordPress in a few operations might hit you with 200-220MB per request, and for an WooCommerce shop, you should already consider separate instance for handling the admin.

If you are going to have a correctly only PHP handling Apache + mod_php, with values at the limit of your hardware resources dedicated to it, you will actually mimic the same that PHP-FPM does and keeps your app much more safe. PHP-FPM gives you the possibility to use Apache, with Event MPM, and set on both sides limits to protect PHP going OOM (Out Of Memory).

To be safe you always end up in using a Web Server to access static files and Proxy to the PHP server, either Apache mod_php or PHP-FPM. You decide which one.

An example for a very small budget WordPress website, on 2GB ram, 2 vcpu:<br/>
1. Use Nginx to deliver static files and proxy to Varnish (give 100m to it), which will proxy to Apache.
2. Set MaxRequestWorkers to 4 (keep it safe for performance of requests, use 2 per vcpu or 4 per real core cpu)
3. Set MaxSpareServers to 4
4. Set MinSpareServers to 3
5. Set StartServers to 4
6. ListenBacklog to max 16 if your HTTP response is > 1s. Adjust depending on how fast are your responses from PHP (not cache)
7. Set Mysql/MaridDB innodb_buffer_pool_size higher if you have loads of posts (10K+ articles or heavy commented blog) but don't allocate more than 768MB as it will take over 70% of ram.
8. Move sessions to Memcached in php settings.
9. Use any plugin that will set correctly HTTP cache headers so Varnish will serve instant cachable pages.

All the above might need the hand of an experienced system engineer, but will make any WordPress website incredebly performant at a 5-10$ monthly hosting fee for a cloud server. Might be a good deal paying somebody a few hundreds to save thousands over next couple of years on expensive hosting.

## Conclusion

Always set MaxRequestWorkers to a value you will not go above physical memory available (consider 20% for OS, or 5% if running in a container, Docker or Kubernetes).

Consider setting MaxSpareServers close to MaxRequestWorkers.

Set ListenBacklog to a value that it is realistic to queue requests.

Consider StartServers to a higher value, as forking new processes is also a bit time consuming and hits the cpu.

A great benfit of using it, is when monitoring system understand Apache HTTPd, but has not idea about PHP-FPM.
