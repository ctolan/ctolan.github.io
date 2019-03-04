---
layout: post
title:  "Quick while Azure CLI downloads"
date:   2019-03-04 09:56:31 +0100
tags: Thinking-Out-Loud
---

As I signed off yesterday I realised I still have content from last week that I want to capture here. Firstly, I’ve kicked off a new project, I know I keep doing that, but this one seems to be a really good way to practice my skills and give back to the community. As I hinted at back in January, I have started writing Pester test for the VMware VMC Module because, well the there wasn’t any. Since, I would like to contribute code to that module (some of the things we’ve created in work), then the best way to build trust would be to write tests for the existing code and then when I add my code it will be demonstrable non-breaking to the existing code. This will hopefully get our team into the main VMware Code repo which would be very cool.

I started at the first function and have been working through them slowly. There are 26 so I’ve a way to go, and the do get more complicated. But I’ve near 100% code coverage for the functions I’ve tested, I know that isn’t the be all and end all but its better than 0% coverage. A picture tells the story best, and no I did not expect to see to failed tests – now I better take a look at that!
![VMC Module Pester Tests image]({{ site.url }}/images/VmcModulePester-1.PNG)

It is certainly different writing tests for code you didn’t write yourself. I had to fight off fixing things that I spotted, because that’s a whole other process when it is someone else’s code. Not that it was a big thing but there were mandatory parameters defined and then an if/else statement for whether the parameter existed – but it could never not exist because it was mandatory. I only bring this up because if prevents me getting 100% code coverage of that function. I can’t get a test to execute the code behind the else. I’ll survive…

I am enjoying the Pester at home – it is fun. I just wish there’d been more of a response to my Pull Request into the project. It has been out there for over a week and not a peep – maybe they’re waiting for me to finish but my whole reason for starting the PR this early was to get feedback on whether they even cared for code coverage in the project. There isn’t that much more to do so I’ll finish this project I promise. It is hard to peel time away from all my other commitments now. I’d love a week off to just sit and code, but that won’t happen I’ve a paper due in two weeks and two other course projects to learn and then build. It is going to be an interesting few months but I’m revving up to full speed. I even feel good about where my thesis idea is going, there is certainly something interesting to explore in it.

Well that’ll do for now, I should get something written tomorrow too, I want to post about introducing my kids to Scratch Jr.

Thanks for reading,

Conor.