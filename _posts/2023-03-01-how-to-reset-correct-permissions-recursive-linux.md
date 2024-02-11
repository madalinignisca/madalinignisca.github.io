---
title: 'How to reset correct directories and files permissions recursive in linux'
layout: post
date: 2023-03-01 13:30
tags: linux files directories permissions recursive reset
category: linux
image: https://source.unsplash.com/LUYD2b7MNrg
---

Here is what you need to do to reset the right way all files and directories in Linux. Works also on Macos and FreeBSD.

![Sad eggs](https://source.unsplash.com/LUYD2b7MNrg)

Open the terminal. Change directory to the directory containing all you want to fix permissions.

We will fix also the owner, optionally.

I am setting OTHERS to 0, but if some services need read access to your directories or files, use 755, respectively 644. I am just a bit more restrictive and set correct the groups depending on how they will be used.

Fix directories:

`find . -type d -exec chmod 750 {} \;`

Fix the files:
`find . -type f -exec chmod 640 {} \;`

Fix owner:

`chmod -R [replace with user]:[replace with group] .`

If this are my local files, usually I replace user and group with my username.

If this are in a web project, on a web server, I set user for the user running the application and group for a group the web server belongs to. I normally ensure both belong to that group. Make note you must set your application platform to do an umask of `027`. PHP it is in the ini settings ;-)
