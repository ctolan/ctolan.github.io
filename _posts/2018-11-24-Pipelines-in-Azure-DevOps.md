---
layout: post
title:  "Pipeline in Azure DevOps"
date:   2018-11-14 09:56:31 +0100
tags: Azure DevOps MSc
---

I got there in the end, I'm calling done for my pipeline. It meets all the requirements with a couple of extras that I hope add enough for a great grade. I put so much time into this because I really wanted to crack it, in a lot of ways this is my new niche. Coming from a Systems Admin/Engineer background handling the deployment of code to the runtime is my wheelhouse. The pipeline also closed a knowledge gap that I had, I must admit I didn’t know exactly the deployed app emerged from lines of code to a built app that was then deployed.

I knew about deploying completed apps, the architecture design, the install and configuration, but not the compile stage. I don’t think I believed it could be as easy as 

```powershell
C:\> MSBuild YOURAPP.sln
```

With that you merely need to add the additional arguments and you have a working app ready for deployment or execution. Yet therein lies the rub, in these additional details is what will make or break your real-world projects. It is the details around the simple command that make it meaningful, it is the difference between hello-world and a working app. Do you only want to run the app locally or do you really need to move it to a server, do you need it packaged in a specific way for the desired platform, and if what about everything else in your deployment runbook? Whatever it is, it is probably possible, but it can get complicated quickly and well that’s the fun. Not that you want complicated, you will refactor it once you crack it, but initially get it working and out the door.


This assignment/project has been great, I do admit I hated it at times when I was completely lost and things that had been working started to fall over and I did not know if it was something I did or something that the tool could not do. Ugh I’m getting flashbacks. Somehow I managed to get my pipeline caught up in an infinite loop, it was building making a change to the repo and then triggering a new build. It was a couple of hours later that I noticed the build number was now in the 300’s and I was not making changes. Looking at a solved puzzle always betrays the difficultly of solving that problem, so I’m kind of labouring this point to get across that it is not as easy as following the examples up on [docs.microsoft.com](docs.microsoft.com).


In a series of posts I will break apart this pipeline and walk through setting up CI/CD from code to app for the C# sample that I am pretty sure you can try yourself because the lecturer has it in a public repo on Github. I might hold off publishing the completed solution until after our class submission date in case it violates academic rules to publish an answer. That’s an interesting point actually, I better change the names to protect the innocent. This course will run again next year and the assignment could be the same.

Ah sure no one is reading this yet so here is a screenshot of the pipeline, beautiful right?

![Full Azure Pipeline]({{ site.url }}/images/Full-Pipeline-1.PNG)

Sonar Qube was a pretty cool new tool for me, since the majority of my code is PowerShell I am most familiar with the [PowerShell Script analyser](https://github.com/PowerShell/PSScriptAnalyzer), this is definetly a post all on its own, I’ll still include the link I followed to get SonarQube working in the pipeline in case it helps anyone.[Sonar Qube Extension for VSTS](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Extension+for+VSTS-TFS)

As I mentioned above there is still a lot of breaking down and fleshing out I need to do, but this is a good start. I’ll need to maintain the context over the series of posted because in isolation if I go deep on a topic it might not make sense. 

Thanks for reading and I hope I’m helping.

Conor