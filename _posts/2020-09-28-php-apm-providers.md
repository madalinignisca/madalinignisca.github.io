---
layout: post
title:  "PHP Application Monitoring Providers"
date:   2020-09-28 09:42:27
category: php
---

This weeks topic is on PHP APM (Application Monitoring) Providers, their features and pricing.
I'd like to come to a conclusion as which one is most suitable to start with.

To tell you from the start, I'm a user of Elastic Stack for observability, and my curiosity was
before they had an apm solution for PHP decent to be used. It is not yet production recommended,
but from testing it the last few weeks, it is more than enough for me.

The main interest of APM is not for development environments, but it's a critical necessity in
production, as it helps us catch early errors, performance issues and a possible bad deployment.

I use mainly APM to be able to discover where code can be improved for performance. And critical is
when I can link a DB query done in PHP to the actual query that run in the database server (to give
a hint on my preference to use Elastic Stack).
