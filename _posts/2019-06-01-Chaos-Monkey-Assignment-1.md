---
layout: post
title:  "Chaos Monkey Assignment Part 1"
date:   2019-06-01 09:56:31 +0100
tags: MSc DevOps
---

As I mentioned in my initial post on this topic (eek nearly two months ago), for college we were asked to create a Chaos Monkey like script to test out HA implementation. That part of the module was teaching us about good decoupled design using message queues and the different strategies available when designing how one system will talk to another. The aim was to demonstrate how with a properly configured Auto-scaling-group (ASG) and a decoupled communication approach the system should be resilient to failures.

This was a really fun assignment for a number of reasons, mainly that it was centred around the Python script and I just don’t get enough opportunity do projects in Python so I enjoyed that, but I also got to work with AWS PowerShell Lambdas, API Gateways and the AWS Simple Email Service too so wins all around. The Python script used the [AWS Boto3 SDK]( https://github.com/boto/boto3) to connect to and interact with AWS components, the documentation is quite good and there are many examples online.

Rough sketch of the process:

- Check that there are instances running
- Ask how many should be terminated
- Shuffle the instances to introduce randomness
- Terminate the desired number of instances
- start a timer to validate the success or failure of the recovery
- Send the results of the test to recipients via SNS subscription and SES enrolment.

Below is the output from the assignment, we were tasked with creating a video demo, recording the video added to the difficulty but it had to be done. Learning how to create a good video is just so valuable these days.
[Chaos Monkey walkthrough playlist](https://www.youtube.com/watch?v=ps67EhdjzBs&list=PL3CTx0aUfJstMxTElKwXfkxX_Sbs_0y42).

<iframe width="560" height="315" src="https://www.youtube.com/embed/5i28HDAefFM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

I am still undecided on just how much detail to go into covering this project but I certainly want to post on what I learned while doing it. It was a great development on what I’d done with AWS Lambdas PowerShell, so look out for an updated post on that soon. The above video is a bit academic and dry, but since it was for an assignment and not entertainment, please cut me some slack it got me an A.

I would be so tempting to kick off this series of posts before completing the pipeline one, but I won’t I owe it to those interested to finish out covering that topic first.

Thanks for reading.
Conor