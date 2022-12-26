---
title: Container image for NuxtJS SSR
date: 2021-11-14 08:30
category: devops
tags: nuxtjs containers kubernetes docker
layout: post
---

You found this article looking in how to make a NuxtJS SSR countainer image to run it either in a Kubernetes cluster or a Docker environment.

Quick tip: it's using [NuxtJS standalong build](https://nuxtjs.org/docs/configuration-glossary/configuration-build#standalone)
and [Docker multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds)

_Article in progress (write any ideas online)_

Here are the steps I took to create a size optimized NuxtJS SSR container image that is fast to deploy and run.

Let's start with the Dockerfile.

First, to be able to build our production ready NuxtJS project, we must install first all the dependencies and run the build. One tip from
NuxtJS documentation is that we can build a standalone version, which should run without all development dependencies. For this reason we
will do a multistep build setup in our Dockerfile to allow us to get rid of the extra storage that dependecies would bring along with our
application.

```
FROM node:lts
WORKDIR /app/
COPY . ./
RUN npm i
RUN npm run build --standalone
```
