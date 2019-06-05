---
layout: post
title:  "Day 3: Azure Pipelines Project"
date:   2019-03-10 09:56:31 +0100
tags: Azure Pipelines BPApp
---

Day 3, ok so I must confess I have been away from this project longer than I expected, but to be fair I have my current class loads as an excuse. Right now I'm opting to do this rather than read another journal article on the state of the art in serverless. For those who care [“Cloud Programming Simplified: A Berkeley View on Serverless Computing”](https://arxiv.org/pdf/1902.03383.pdf) was really good, hot off the presses released last month.

When I finished last time we had just published the app to Azure’s free tier hosting. The code is still a mess, the links to the app do not work, but we published it in no time at no cost. Today I want to bring a pipeline into the projectm Azure DevOps (as it is not called). Following on from [where we finished]({{ site.url }}/Day-2-Azure-Pipeline-Project/) in Visual Studio Community edition, literally on the same panel where we published to Azure if the link to configure Continuous Delivery (to at least get us started).

![Configure Continuous Delivery image]({{ site.url }}/images/Day-3-Continuous-Delivery-1.PNG)

Using a GitHub repository is new this time around and so is this warning message. Not a big deal it turns out, Visual Studio needs a token to connect to GitHub APIs.
![CD GitHub Token image]({{ site.url }}/images/Day-3-CD-GitHub-Token-1.PNG)

Click the blue link in the error message and it takes you to your GitHub account. There click “Generate new token” and as instructed by the message in Visual Studio, grant this token “repo” and “notification” scopes.

![CD GitHub Token image]({{ site.url }}/images/Day-3-CD-GitHub-Token-2.PNG)
![CD GitHub Token image]({{ site.url }}/images/Day-3-CD-GitHub-Token-3.PNG)

Oh well gotta stop here – running into an account issue, possibly related to replacing my CC recently. --- WIP ---

Thanks for reading.
Conor