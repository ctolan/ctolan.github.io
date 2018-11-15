---
layout: post
title:  "Why I love PowerShell AWS Lambda"
date:   2018-10-14 09:56:31 +0100
author:
  twitter: ConorT
tags: PowerShell AWS Lambda
---

I executed the function from the main page once created and it works!
![AWS PowerShell Lambda Works Image]({{ site.url }}/images/PowerShell-Lambda-AWS-Works-min.PNG)

So it works now what will I do with it. The main reason I get so excited about PowerShell Lambdas is that it recognises PowerShell a 1st class citizen in the cloud. I am from a Microsoft background and have used PowerShell for AD tasks, Exchange Administration and then PowerCLI for VMware automation. PowerShell is the only language I would be able to use for all those platforms, I know there is decent python support for VMware these days but come on, really? Nah I'd be mad to have learned anything but PowerShell. Yet as everything moved to the cloud and Windows and servers became passé I felt left out to be honest because I haven't mastered Python or JS, I've mastered PowerShell.

Don't get me wrong i can read and write in those languages but i think in PowerShell as my first language, and i know that it is a modern language but it never makes the [StackOverflow Developers Survey list of most popular languages](https://insights.stackoverflow.com/survey/2018/#technology-programming-scripting-and-markup-languages) I mean it can't be that niche is it? Also, it isn't that they're excluding scripting languages because look it’s in the title, they're even including markup languages. So honestly, I do not get the lack of recognition from the development community. I think some of it is Microsoft hate following the language around.

But anyway, we've made it now! Microsoft put so much effort into breaking away from being Windows only and you must admit they've pulled it off if AWS are supporting PowerShell lambdas. So why is this worth being excited about, well I'm getting there I hope. Now that I have somewhere to run serverless PowerShell functions I can write application logic in PowerShell and have static websites residing on S3 or another static site hosting. I can do complex computation in PowerShell which as I say is my natural language. I have played around with Python and the Django framework, and I've played around with JScript, but they are harder for me to think in, so it's harder for me to create new things. Now I feel I can unleash all the smaller apps I think of with without the hurdle of standing up a windows server and the associated costs for licenses not to mention ops and patching. I get ops with my day job I don’t need them for my hobby too. I just want thinks that scale naturally if anyone else starts to use them. It is the Pay As You Go model that is missing from the IaaS model.

For example I love my Home Automation and Alexa skills can be a trigger for Lambdas. So I can write whatever in PowerShell to trigger a light buld or read info from a sensor and connect that up to Alexa for voice activation or read back.

What will it cost? Very little, far less than running a server 24/7 that is for sure. From what I've read on [the pricing site](https://aws.amazon.com/lambda/pricing/) suggest that I will remain on the free teir for a long time. I should be able to get a few apps or Home Automation tasks for free, and if not I'll let everyone know.

In conclusion it is the cost/scale angle,the recognition of PowerShell as a real web/cloud language and my entry point into serverless that has me so excited about PowerShell Lambdas.