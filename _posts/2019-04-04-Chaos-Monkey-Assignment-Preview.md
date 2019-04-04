---
layout: post
title:  "Chaos Monkey Assignment"
date:   2019-04-04 09:56:31 +0100
tags: MSc DevOps
---

For college we were asked to create a Chaos Monkey like script to test out HA implementation. This was a great project to work through, I used the AWS python SDK Boto3. Quite a small learning curve and I think I can cover the bones of it in one blog post once the assignment is handed in. A real world addition to causing chaos was to time the recovery and send a message either via a lambda or via a SNS topic. This took a little fiddling but again it was great to get hands on with a “real” problem to solve.

AWS really makes things very straightforward for developers, it is shocking easy to get your credit card out and have things up and running with just a little bit of effort. This get you started but I’m also aware that none of my demo apps are anything close to safe for an enterprise. What AWS can’t as easily solve is the chasm between POC and MVP, where the V caries the significant weight for an enterprise. What is viable for an individual with a home business is not viable for Fortune 500 company, it just isn’t. Oops I got side tracked there on a bit of rant I’ll reign myself in.

Chaos, yes chaos, it is quite the challenge to think about implement something like this in work, in Prod. I mean sure we’ve built highly-available systems and have plenty of redundancy but still, do we want to intentionally risk impacting our customers? During a problem investigation a few years ago, we were going around and around making presumptions about the root cause of an impact. Was it X or Y? Yet when I asked if we could try rule out X by executing it under a controlled condition of Y not changing, the idea was shot down. Could it be better to remain in the dark about the root cause of the outage than confirm it. To quote the [Google SRE book]( https://landing.google.com/sre/books/) “Hope is not a Strategy” and yet business impact must be avoided. End of the day X was disabled, and everyone hoped that there would be no more outages. I really wish I could have confirmed it is was or wasn’t X before we moved on.

It really must be a confident team who can say sure go ahead wipe out as many instances as you like, my infrastructure will rebound. The code to wreck the infrastructure is easy to write, the defence is not so easy. I’ll write up the Chaos Monkey project in a blog soon as the college semester is over, I’m absolutely up to my eyes at the moment with projects and work. Fun times.

Thanks for reading.
Conor