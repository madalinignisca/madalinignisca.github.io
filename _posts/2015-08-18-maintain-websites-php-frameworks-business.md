---
layout: post
title:  "Maintaining inherited websites on different PHP frameworks, a business opportunity"
date:   2015-08-18 06:50:00
categories: general
---
Not all of us are lucky to end up in startups that are building really awesome web/mobile applications.

Some of us end up for a good amount of time in maintaining and extending already made applications in or for various digital agencies.

_This comes with both with good and bad parts._

I've been involved in the last period working on some web applications built on some pretty known classic PHP frameworks and pushed me to reorganize my personal time to learn new things I haven't done yet.

The good part is short, you're happy with results when you get things working, but it's the less amount of time. The most amount of time is with frustrations. Anyway, on long term, this experience will give the developer an advantage in the future.

As most of the time I've spent on creating websites and being involved in a few web applications started from scratch, I was used to work by following the recommended ways in the framework or CMS that was used. I'm one of those who likes to stick to the rules and have order in what he works on and most of the people I worked with, remote, were sharing some similar principles.

So digging into some inherited web applications, some older then 4 years, has put me in a new situation. Maintain code written in chaos. Code written by how each person considered to do it. Hacks to just get a certain result, no matter that it's not easy maintainable, and with no tests at all. Security? No considerations into it. Performance? Not a single chance. Documentation on code and projects? Why would that be necessary?

So, I'm not a "giving up person". As I do usually, I started by researching and reading the official documentation, some recommended books, some discussions on the official forums of the PHP frameworks and just in a few days, I was able to do fixes and new things as required.

But one huge problem came up. Doing fixes and adding new stuff, required many times from additional minutes to hours to refactor many parts from the way they were done. Most of the time, the estimated time on doing a task was not reachable. Because refactoring bad written code can take more time then coding something from the start.

When I moved to UK, based on many things I read on the internet on what is demanding for most of PHP developers (I used Jobsite.co.uk for this) I was expecting to find here something like an ideal software industry ecosystem. Well, the disappointment is that even if the presentation of the companies sounds like it should be, in most of the time it is the total opposite.

So my opinion in why is this happening is pretty simple. I think that between business people (includes managers from clients and service providers) and the actual senior developers / project managers there is a big gap that can assure that a project is done the right way. Business people want to see results. If quality is on paper and in words, that doesn't mean that it will be in the Code as well, and they don't know that.

In job proposals that I receive in my email I see most of the time that the developer should be able to work in an Agile environment, do Test Driven Development, and other stuff. Disappointment is that most of the time those words were put there by recruiters just to make the hole text sound great (and I bet is for the eyes of their clients).

And something ironical about it. Almost all stuff related to PHP and JavaScript that I have learned is from books written by UK based developers. So my wonder, is, why some people from here, that are so close to good quality resources and would be able to go to local meetings where people that adhere to good principles in writing code gather and chit chat our non-sense development stuff, don't take this opportunities and just do their thing, take the money and get lost. Is it so hard to take a path to improve and do quality stuff?

Web development has evolved a lot. There are great tools online that can help in making sure that everything is in perfect order. They been available for years. Their costs are low. Just take a look on how a continuous integration tool and a unit testing can help in making sure that the actual code does what is supposed to be doing and passes all required tests.

One thing that I found in a previous team that I've worked with, was that the project manager was really away on how to proper use some testing tools. He wasn't even able to create theoretical scenarios for the components that were built. Well, anyway, he was the best friend of the agency manager and we the other three developers were just the "workers", in their eyes they were superior to us and our considerations were not important (because he wasn't able to understand those things). The result of the final product was in my opinion a disaster. Like usual, after delivery, to extend different areas, the new estimations made the client aware that something was not in order and the promises that the app would have been done in a proper way was just a lie to get the money. But he and the managing director were marketing themselves as working in an Agile manner and being experts in TDD.

And I bet that this scenario is met in many other occasions.

_This gave me an idea of a business._

**Where is it starting?**

There are lots of companies (small and medium size) that have outsourced their projects. For many of them, they ended up in a similar situation, where they have a web application, started on one of the popular PHP frameworks (Zend Framework 1, Symfony 1, Code Igniter 2, Kohana 2 or 3, Yii 1 etc.), that are supposed to be done by best practices, but they ended up without support from the initial teams for various reasons: most developers left the team as they want to work on more recent modern frameworks, initial service providers can't solve and deliver fixes and new add-ons on time or even can't do them, more money are demanded so they would be forced to start over again on their projects, as the agencies as are hiring new people, those are more comfortable on more recent frameworks and components.

By having an application started X years ago, on an older major version of a framework doesn't means that it needs restarted on modern frameworks next day. New frameworks come with new concepts in doing the same thing, on most of the included stuff, and it doesn't means that it improves things. Don't contradict this, as most of the concepts in them are older then our age already, they just got implemented in. There are concepts and algorithms. Example? Most ORM components included in frameworks that are based on Active Records pattern or Data Mapper pattern, that are like over a decade in age and most classic frameworks implementations are younger then the patterns. So if you have Kohana with it's ORM, it doesn't means that starting with Laravel and it's Eloquent ORM component any major things will change. Using cache in an app was possible and it is done by an exact similar pattern in any other framework. And just that it misses an easy way to have migrations, it doesn't means that it's hard to do it; really it's a few minutes thing.

The reality is when you have an old project and you search for a new development service provider that would be able to maintain it, if you get in most situations proposals of rewriting it, is because they just got used to another recent framework and they aren't interested into getting their hands dirty and spend time learning a bit of some practices used in the framework version used in your project. And another huge problem, if it is supposed to be in a certain framework and version and the actual application code has nothing to do with it.

_About code that has nothing to do with the framework initially used_

I worked once to build an API for an application built on Code Igniter and I found that I could not use anything from the already done code. The team that worked on it they did not use a single thing specific to Code Igniter. They coded pure PHP specific code not reusable at all; you could find even manally made mysql connections and hand made queries. Even if I promised an amount of cumulated hours (those I've billed) I had to put twice effort and hours to do something. I ended up creating a separate application, made all necessary models, made all base helpers that would allow building the most common stuff you expected (I've learned a lot at that point from some good books written by Jamie Rumbelow, a great UK php developer) and the API was working and not only. To add new functionality was a piece of cake in my app even for a junior developer, but in the actual website app, was close to impossible. So I created what should have been in the app from the beginning and everybody should have used and write half the amount of code. It would have been so easy for anybody to join the continuous development process that was intended by the client for the next few years.

**What would my business offer?**

Support for this kind of web applications (well, most would be websites called by most of people).

Host them in a protective environment and adapted to their needs. Refactoring critical parts and take care of all security improvements. Extend and implement caching mechanism to lower hosting costs.

Plan ahead on maintenance and refactoring areas that should have been done in the framework specific way. Document the application and offer the possibility to extend it at a normal price range that should be.

Communicating with a team of people that share a similar vision and gained experience in those frameworks over time.

Something still desired by companies (well, most in UK, less in rest of the EU), old browsers compatibility, especially Internet Explorer 8, even 7 and 6, and huge patience to explain the client what is Progressive Enhancement or Graceful Degradation and why is it best to be done within one of this principles (based on how the project was started and how it could be improved). Ah, yeah, not to forget, posibility to extend the website to be responsive and adapted to most popular mobile devices.

**Why do I want to do this?**

As we get older and we gain more experience we start to think different, we have more patience, we gain more empathy etc. We become better I think.

I don't want to spend the rest of my life by continuous learning new stuff that would be just the same things rewritten in a different way and forcing to do things in a different manner just to achieve the exact same results.

I would like to work with people that share common ideas and visions and that we have been learning and working for a similar amount of time.

I consider that some of the classic frameworks still deserve a chance and can be maintained and improved for another good amount of time. They were the foundation of the "cool new stuff" is used currently, many of them being just forks out of them, having a different name, hiding it's past, with people that act as they created them from the scratch. There are already "modern" frameworks that as fast as they came and made noise, same they silently disappeared.

I don't agree with people that think that some things are easier to be done in the more "modern" ways. They just prove that they can't do more low level programming. It's PHP, you can do anything, well, almost, can't do coffee yet with it, but I'll find a way.

If you look at the major important frameworks, you would discover a different mentality. Just try to read more on the history of frameworks like Zend Framework, Symfony, CakePHP, Code Igniter or Yii (and some other to be considered). They were since the beginning of PHP frameworks and they will be even 25 years from now. We can't say the same things about the frameworks that started as forks from them.

**Why would a company prefere my services**

I am a developer. I am a developer that set the foundation of a team that shares a similar vision. We are here to stay. We won't bug you with the idea that the app must be written again in a new framework, or even a new programming language. We belive in good refactoring and easier porting to newer technologies.

A predictable buget for your application maintenance, hosting and improvement.

We know to manage the project in a modern and human understandable way (we won't freak you out with tools that look like from Star Trek for you).

**What will involve this?**

A good amount of time would be to be more involved in some of the frameworks I like and a small team with people that share the same ideas.

If you're into the same concepts, let me know (remote work is considered for people that like to travel while they work) or if you have a project that is in the situation of what I described in the article, don't hesitate to contact me.

**Let's talk about it and get things done the proper way.**
