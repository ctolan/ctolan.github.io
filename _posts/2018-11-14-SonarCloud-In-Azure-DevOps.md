---
layout: post
title:  "SonarCloud in Azure DevOps Pipeline"
date:   2018-11-14 09:56:31 +0100
tags: Azure DevOps MSc
---

I have been quite impressed by SonarCloud, I did not have previous experience with SonarQube so this is all new to me. As I've mentioned in a few posts, we were asked to implement quality assurance into our pipelines with N-depend or SonarCloud. I went with what I guess is QAaaS? SonarCloud as a hosted service allows me to check the quality of each build and I added tasks to the pipeline to break the build if the project does not _Pass_.

![Azure New Web App Image]({{ site.url }}/images/SonarCloud-Azure-Pipeline-1.PNG)

Right out of the box you get a lot for your efforts. There is a default min standard profile that get applied called the Sonar way, and it will start checking your project against 100's of rules for various languages.

![Azure New Web App Image]({{ site.url }}/images/SonarCloud-SonarWay-1.PNG)

Here you see that the default code coverage should be greater than 80%. This forced QA is more than a nice to have in my opinion, forcing conformity raises the bar and will keep standards high. Yes it'll be a pain to have to hold off pushing code that doesn't meet the standard but sustainability and maintainability are really important. You should not be pushing quick hacks and last minute subpar code, so take the time, set something like this up and enjoy knowing that it will be worth it in the long run.

![Azure New Web App Image]({{ site.url }}/images/SonarCloud-Rules-1.PNG)


I'll leave this link here for reference, it is what I followed to get it working in my pipeline [SonarQube Extension for VSTS (Azure DevOps)](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Extension+for+VSTS-TFS).