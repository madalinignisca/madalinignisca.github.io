---
layout: post
title:  "I discovered Serverless and I've fallen in love with the concept"
date:   2017-12-27 08:10:00
categories: coding
---
<p>Over the last few days I started to read about <strong>Serverless</strong>.</p>

<h3>What is Serverless?</h3>

<p><strong>Serverless</strong> is a different way of building (Web) Applications.</p>
<p>Over the last few years, on emails from the AWS newsletter, I kept seeing <strong>Lambda</strong> mentioned a lot so I started to look into it.</p>

<h4>What is Lambda?</h4>

<p><a href="http://docs.aws.amazon.com/lambda/latest/dg/welcome.html">AWS Lambda</a> is a Function-as-a-Service (FaaS) compute service.</p>
<p>You write functions that would be triggered based on events, like an http call, or a file upload on S3 or anything that can somehow communicate within the cloud provider, in this case Amazon AWS.</p>
<p>The next thing that captured my attention was how it is priced: you pay only when it is running! For sure, instead of having a locked price on some vps instance or some other way of hosting, you pay only when the function runs and based on how much resources it had consumed (cpu, memory) for an amount of time.</p>
<p>The other important thing is that it scales as needed and you control the limits (you do not want to go broke if not making a profit from your App).</p>

<h4>So Serverless is some AWS thing?</h4>
<p>So within the lecture about Lambda, I've started to see mentioned <strong>Serverless</strong> as a framework. And next was that not only AWS does it, but Google Cloud and Microsoft Azure as well, each in it's own way, but following the same principles.</p>
<p>So I discovered that there is also a framework around the concept, named <a href="https://serverless.com/learn/"><strong>Serverless</strong></a> that helps developers concentrate over the logic and easing the infrastructure management.</p>

<h3><em>Wait, I thought you've said that you do not have to manage any vps or other hosting solution?</em></h3>

<p>Right, you do not. But your code, data and possible files need to go somewhere.</p>
<p>You can look at the Serverless framework as to a tool that helps you skip all the complicated settings you need to do and tweak in the "help I've lost my self" AWS, GCH or Azure panel.</p>
<p>Providing minimal details, it will automate the deployment and creation of necessary services and configuration and you'll enjoy your app running fast, even integrating it with some cool CI/CD service that you like.</p>

<h3>So for what would I use it?</h3>

<p>Short: for any possible event your application needs it.</p>
<p>A RestAPI, converting images when a user uploads one, sending a notification to all subscribed users of your website, etc.</p>
<p>The idea is you would use it for all you've done until now with your website and mobile app, and many things more that your current tools where limiting you.</p>

<h3>What's next?</h3>

<p>So my next task is to wrap up a simple web application skeleton and have some authentication with it.</p>
<p>The setup will be a minimal SPA hosted on S3 with Cloudfront that uses <a href="https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html">Amazon Cognito</a> for authentication and implements a registration and login system for now.</p>
<p>This has lots of little steps to play around and will keep this in the journal how will go.</p>
<p>After that, will see what can we plan.</p>
