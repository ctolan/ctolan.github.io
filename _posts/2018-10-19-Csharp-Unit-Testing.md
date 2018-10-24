---
layout: post
title:  "C# Unit Tests"
date:   2018-10-19 09:56:31 +0100
author:
  twitter: ConorT
tags: C Learning
---

For this semesters college project we are tasked with implement continuous software delivery through a pipeline performing unit test, integration tests, user acceptance tests and performance tests. It is a great project, I'm actually excited to get to do it. We have been given a mostly completed C# application that calculates your blood pressure and we've have to complete the program, add a feature of our choosing and create the continuous delivery pipeline with all the bells and whistles we can muster.

I got the app working today after completing the small bit of additional logic necessary to return your blood pressure given the systolic and diastolic input values. I would not say that the code was complex but the syntax of C# apps is still new to me. I know that I'm becoming a software engineer but I'm acutely aware of my inexperience with what I expect is common knowledge in a recent Comp Sci graduate.

Once I had the application running I moved to the next task, writing unit tests to get code coverage up to a reasonable number. I'd heard 70-80& put out as a good target, but recently heard that Microsoft target 60% now because above that the return on investment is not worth it.

It took me a while to get the hang of unit tests in C# because it is quite different to the Pester PowerShell testing framework that I am most familiar with. Comparing the two, I can say that testing in Pester is harder than C#, at least in the context of this app and with the assistance of Visual Studio 2017 (we get a student license). The bit that put me off at the start was having to instantiate the new object first before setting the properties. Purely my learning curve coming from PowerShell, once I had my object setting the properties and testing was easy.

After getting 4 or 5 basic tests to get the code coverage up I still wanted to test invalid range of input. I'd seen an example testing invalid parameters where they added and additional parameter and it raised a parameter exception, but I needed a range exception or a validation exception. I searched and searched but didn't find what I needed, in the end I’m not sure if it is the way the app is written because it doesn’t really throw and error on invalid range. Instead it changes the output message but it isn't a thrown error, the site continues without crashing.

The next step for this project is to get the pipeline working in [Azure DevOps](https:// https://devops.azure.com). I started, my remote repo is all set and my builds are successful, but I ran into a wall with deploying. I need to learn the Azure way of doing things, I wasn’t sure what exactly the Azure Web App Service name should be, when I tried making one up it failed with a “resource does not exist” error. I believe I need to create a pool of resources to deploy the app to, or point at some other service name for shared hosting. I’m not really sure yet.