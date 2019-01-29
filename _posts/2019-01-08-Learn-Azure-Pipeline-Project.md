---
layout: post
title:  "Learn Azure Pipelines Project"
date:   2019-01-08 09:56:31 +0100
tags: Azure Pipelines BPApp
---

Here it is, the start of the Azure Pipeline project series that I’m going to publish for others to follow along. This was a college assignment which I particularly enjoyed and found useful in the new age of DevOps. I found it so good I felt compelled to share it. It is hosted on Azure and can be done entirely on the free tier, for my college project I used some paid features but I've rolled those back now and it is still as good as ever. This series will walk through all the steps to get your own CI/CD pipeline up and running on Azure for free. This is a great opportunity to get hands on and learn the fiddly bits yourself, in may large organizations these details are kept behind the curtain and you miss out on knowing how they actually work (it is easier than you probably expected). So let’s jump in with an opening post setting out the App and the Ask, I will follow up with the first steps post shortly.

# DevOps CI/CD Pipeline Learning Project

## Project Application

Your blood pressure is calculated from your Systolic and Diastolic readings. Given these two numbers, your blood pressure is classified as Low, Ideal, Pre-High and High.

![BP Chart image]({{ site.url }}/images/BPChart.jpg)

![BP App Snip image]({{ site.url }}/images/BPappSnip.png)

## Project Outline

Joining a team with a mostly complete [ASP.NET Core](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-get-started-dotnet) web application, the challenge is to design and configure a Continuous Integration and Continuous Delivery pipeline in the [Azure DevOps](https://dev.azure.com/) / [Azure Public Cloud.](https://azure.microsoft.com/)

You are tasked with getting the project into a better DevOps posture. They need a CI/CD pipeline that will meet the following:

- [Continuous Integration](https://docs.microsoft.com/en-us/azure/devops/pipelines/build/ci-build-github%3Fview%3Dvsts) - The application is [built and tested](https://docs.microsoft.com/en-us/azure/devops/pipelines/test/getting-started-with-continuous-testing%3Fview%3Dvsts) on each push of code to the repository. [[unit tests](https://docs.microsoft.com/en-us/visualstudio/test/getting-started-with-unit-testing%3Fview%3Dvs-2017) and [code quality/static analysis](https://sonarcloud.io/)].
- [Continuous Delivery](https://docs.microsoft.com/en-us/azure/devops/pipelines/apps/cd/deploy-webdeploy-webapps%3Fview%3Dvsts) - The application is deployed and undergoes automate User Acceptance testing [[Selenium](https://docs.microsoft.com/en-us/azure/devops/pipelines/test/continuous-test-selenium%3Fview%3Dvsts) and performance tests].
- Expected behavior - a developer pushes new code and so long as [all tests pass](https://docs.microsoft.com/en-us/azure/devops/pipelines/test/review-code-coverage-results%3Fview%3Dvsts) the update is published to the Production WebApp Url.
- If the code quality is too low, or the Web App functionality (UAT tests) fail then the build should fail and not be deployed to Production.
- Optionally – continue development of the application and add a new feature of your own creation (include tests).

--------------

## High Level Tasks (not in any order)

- Get [Visual Studio Community edition](https://visualstudio.microsoft.com/free-developer-offers/) / [[Macs](https://visualstudio.microsoft.com/vs/mac/)].
- The application is incomplete and will not build. Write the missing code in line with the specification of the chart above, and be able to develop locally (Ctrl-F5 to launch locally). Review the code in the [BMI calculator app](http://bpcalculator-2-prod-as.azurewebsites.net/) for help.
- The application has no unit tests, add a test project and [write some tests](https://docs.microsoft.com/en-us/visualstudio/test/unit-test-basics%3Fview%3Dvs-2017). Test locally with [Test Explorer](https://docs.microsoft.com/en-us/visualstudio/test/run-unit-tests-with-test-explorer?view=vs-2017).
- Stand up an initial build pipeline to pull the code from the repo.
- Stand up a release pipeline to connect to Azure and publish the app as a [Azure Web App](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-overview). You can run up to 10 [Web Apps for free](https://azure.microsoft.com/en-us/free/) so it should not cost you anything to run a Dev and Prod web app.
- Write some Selenium tests to imitate user behavior, (enter data – check for correct output).
- Fork your own copy from [https://github.com/ctolan/bp](https://github.com/ctolan/bp) to Azure Repos or GitHub (both can be a source for a Azure Pipeline).
- Improve your pipeline, be sure Production is not affected by a bad development deployment.
- Consider a load balancer in front of multiple instances of the App for High Availability. Can your app survive a region outage?
- Improve code quality – get a [SonarCloud.io account](https://sonarcloud.io/) and configure your project for analysis (free if project is public). Fix or exclude the issues found.
- Configure continuous quality testing by configuring a quality gate in the build pipeline to break the build if not good enough.
- Set up a [Google Analytics account](https://analytics.google.com/analytics/web/) and add the Web App for insight into customer usage and demographics. Do you need a notification about cookies now (GDPR)?
- Ensure necessary test files from build are packaged with the “drop”.
- You can add script (PowerShell) tasks that will print out (Write-host) "dir" to the logs.
- You can use copy, zip and extract tasks if needed.

## Notes

This is a task I was assigned on a college course and felt it would be valuable to share. This took many days and nights of work it is not something you will complete start to finish in one sitting it is a project that you will develop over a few weeks of work as you learn as you go.

This is an interesting personal challenge that anyone can undertake to explore and experiment current DevOps tools and practices. When written it was possible to do all of this on the free tier of Azure, but this may change.