---
layout: post
title:  "Selenium Tests in Azure DevOps"
date:   2018-11-13 09:56:31 +0100
tags: DevOps MSc Azure
---

 After several days bashing my head against my Azure DevOps pipeline, I finally got the Selenium tests working. Hindsight being what it is, it seems easy to understand now but I struggled. I knew that Selenium tests needed to be run against a deployed WebApp so I was putting them into a stage in my Release pipeline, but kept running into "no test assemblies found" errors. Actually, as I write this I realise I should get the error message correct in the hope that I can help someone with the same problem.

What was the problem I hear you ask, well the test assemblies were not deployed with the webapp. Either because they are test assemblies or because they were in a different folder when it was zipped up. I must admit not knowing which at this time. I had to resort to echoing “pwd” and “dir” in the logs to try find my way around the deployed host. In one way this was good to do because it closed the loop for my that the Azure Pipeline could be worked in the same way as a Jenkins Pipeline but with PowerShell instead of bash. This was a great but being able to list all the files and folders didn’t explain to me where my test assemblies were. The tutorials and guides I was following were all for VSTS which seems to have employed a single pipeline where you have Build and Deployment stages together, and the test assemblies would have been referenceable. Or at least they were in the examples I was looking at.

I spent a lot of time now knowing whether I was doing something wrong or just didn’t know what I was doing at all, tough times. Eventually I tried running the Selenium tests in the build pipeline where I knew the *Test*.dll existed (because the unit tests work there) and made progress. 

It is wrong to do a build of code and then to run Selenium tests against a previously deployed version of the WebApp but at this point I just need to know that I can run the tests, that they work. Because there are all the other things that I had to do to get this working that did work, but it’s the one that didn’t that leaves a mark. For example there is changing reference to the chromeDriver so that it points to the one that is actually on the Azure host, but that is covered in the Documentation quite well. 

Oh and let me not to forget I also spent days working with the wrong test project altogether. I created a Unit test project (.NET) instead of an xUnit (.NET Core) project. I was running into all sorts of missing package problems along with my missing assemblies. Ugh.
[nUnit vs xUnit Project Image]({{ site.url }}/images/nUnitVsxUnit.PNG)

Where does all this leave me, I need to copy over those .dll’s to the deployment package location prior to it being zipped (as was actually shown in the sample code from the lecturer). Lesson learned on this one, stick to the lecturers provided material first and Google second. I have to assume he completed the project himself before assigning it out to us. So he knows it is possible to accomplish.

Much more to do with this pipeline, I need to put some real thought into the stages and flow but so far I hve been focused on learning what is what and getting the bits working.

Thanks for Reading,
Conor.