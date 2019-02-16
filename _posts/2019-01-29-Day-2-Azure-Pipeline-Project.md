---
layout: post
title:  "Day 2: Azure Pipelines Project"
date:   2019-01-29 09:56:31 +0100
tags: Azure Pipelines BPApp
---

Day 2, I decided that it will be most beneficial to more people to see how to get this into Azure DevOps rather than going into writing application code for an application that no one really cares about. So here we go. I have re-opened Visual Studio and opened my project. Why not "Launch" it again to make sure you have working code to start with.

![Visual Studio Community image]({{ site.url }}/images/Day-2-Launch-1.PNG)

Success. Stop it with the Red Square on the tool bar at the top of Visual Studio. For those wondering why Visual Studio, you are about to find out. In the Solution Explorer select “BPCalculator” -- “Publish” -- “Start”

![Visual Studio Community image]({{ site.url }}/images/Day-2-Publish-1.PNG)

The publish target is Azure App Service, the starter application is .NET Core so it is compatible with Azure App Service. Click “Create New”.

![Visual Studio Community image]({{ site.url }}/images/Day-2-Publish-2.PNG)

This next page is important, you want to be sure to choose the “Free” hosting tier. Click New beside Resource Group and give it a nicer name.

![Visual Studio Community image]({{ site.url }}/images/Day-2-Publish-3.PNG)

Then Click New beside Hosting Plan and choose a location which makes sense for you, I’m in Ireland so that is Europe North, and then be 100% sure to select the “Free” (F1) tier. It is perfectly fine for what we need.

![Visual Studio Community image]({{ site.url }}/images/Day-2-Publish-Free-1.PNG)

Once you are sure hit “Create”, let Visual Studio its thing then click Publish.

![Visual Studio Community image]({{ site.url }}/images/Day-2-Deploying-5.PNG)

It will compile you project and connect to the Hosting plan that you just created, since we are using a known format and serivce to the Visual Studio it takes care of everything for you.

![Visual Studio Community image]({{ site.url }}/images/Day-2-Deploying-2.PNG)

![Visual Studio Community image]({{ site.url }}/images/Day-2-Deploying-4.PNG)

If successful it will show the Site URL and even launch the site for you.

![Visual Studio Community image]({{ site.url }}/images/Day-2-Deploying-Success-1.PNG)

You will recognise this as a out of the box Visual Studio site. Our custom project page is at /bloodpressure.cshtml. So if I append that to the URL I get my page/webapp.

![Visual Studio Community image]({{ site.url }}/images/Day-2-Deploying-Success-2.PNG)

Ok so we are not at CI/CD yet but we have gotten our WebApp published to the internet for free, that is pretty impressive as far as I'm concerened. You can rework this app to do whatever you want, whatever you're capable off. Then Azure will host it for free allowing you to show off, test out a new idea, practice writing C#, practice web app development, whatever you are after you've launched something online in two days.

From here we need to add the CI/CD, and depending on the order you are following these posts in you may want to get into code and fix up the app code. What not add you name to the page and publish it again with the update?

Thanks for reading.
Conor