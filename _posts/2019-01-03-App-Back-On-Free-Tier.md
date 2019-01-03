---
layout: post
title:  "App Back Up On Free Tier"
date:   2019-01-03 09:56:31 +0100
tags: Azure Pipelines
---

My first task of this 2019 was to submit a paper which we had extended till today, so I submitted that last night. Next up, now that I'm free and clear of course work is to revert my blood pressure app back to the free tier. I got a bill of just under 60 euro for my Azure usage towards the end of last year.

Knowing that I can run 10 free web app services I intend to make use of them for my portfolio of apps. I had deleted all of my Azure resources to close out my billable hours, so first thing was to re-create the App Service on the [Portal](https://portal.azure.com/).

![Azure New Web App Image]({{ site.url }}/images/Azure-New-Web-App-1.PNG)

Above you can see it is quite straight forward, I entered the App name, chose my subscription, resource group and configured to use a free tier App Service Plan.

With that up again I went to [my pipeline](Devops.azure.com) and adjusted the tasks to line up with the correct App Service name. I have two, one for Dev and one for Prod as denoted in the App name. This is so that any changes get pushed to the Dev URL first and can be tested. If they pass then they can be deployed to the Prod URL, but if they fail I don’t have to roll back my deployment - the Prod URL is unchanged.

![Azure Web App Pipeline Image]({{ site.url }}/images/Azure-Web-App-Pipeline-1.PNG)

It is a reasonable release strategy for what i need to do. If i only had one URL any bad code would take down my app until I fixed it and giving I'll only be dipping in and out of this that would be poor customer experience. Even if i was paying for a Prod quality service I would still use this free tier for testing. Trust the construction of your pipeline, put all the logic in there to make deployment a safe and repeatable process. Add tests for all new things that you expect to work and you should be all set (I know easier said than done).

I will need to adjust my own tests since the free tier does not support custom domains, in my college project I had a post-prod validation test task to check my site was up on the custom subdomain.

Here it is [my Blood Pressure Category App](http://bpcalculator-2-prod-as.azurewebsites.net/). I am working on getting basic forwarding working for the old custom DNS name bc.conortolan.com going again. I liked how memorable it was, I have my next App idea ready to start shortly and will use something similar.
