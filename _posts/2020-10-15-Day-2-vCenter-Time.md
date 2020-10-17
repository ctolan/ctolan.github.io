---
layout: post
title:  "Day 2 vCenter Time"
date:   2020-10-15 09:56:31 +0100
tags: HomeLab
---

As I had hoped it was actually quiet easy to get the vCenter installed and I did infact know what I was doing, mostly. I knew I'd need to get an ISO from VMware for the VCSA, I downloaded that and created a VM before having created a datastore. This is something I've really apreciated about the build, all the parts work out of the box. My thanks to those who have gone before and figured all this out. Hat tip to VMware and Intel for making it happen on the product side, so take my money.

![Datastore creation image]({{ site.url }}/images/New-datastore.JPG)
![Datastore created image]({{ site.url }}/images/New-datastore-2.JPG)

Datastore created, I figure 500GB would be enough. Next I went down the wrong path of copying the ISO to the datastore and then I created a new VM and tried to mounth the VCSA ISO. The VM didn't boot, that's not what I should be doing. After a bit of documentation reading I realised that I needed to mounth the VCSA ISO locally on my laptop and then open up either CLI installer or the GUI installer. I went with the GUI this time. Ran into a this error when clicking through the setup, its these little things, I didn't know that for a production setup I'd need a full 500GB minimum for the VCSA. That could be trip up question in an exam for sure. It'd seperate those experienced installing vCenter from those who aren't.

![Datastore created image]({{ site.url }}/images/deploy-vcenter-1.JPG)

No big deal for my homelab to go with thin provisioning, so no issue. So we're off with step one, deploying the vCenter VM to the homelab. Then step two configuring the vCenter appliance and then done. It is deployed and configured with an SSO domain and the config that I suplied via the GUI. Nothing exciting so I'll not go into detail.

![Install Stage 1 image]({{ site.url }}/images/deploy-vcenter-4.JPG)
![Install Stage 2 image]({{ site.url }}/images/deploy-vcenter-5.JPG)
![Install Stage 2 Complete image]({{ site.url }}/images/deploy-vcenter-6.JPG)

What I love about this is that the vCenter has no awareness of its host or the platform on which is runs. I have my own vCenter now running with no hosts and it has no idea that it is even a vitual machine. In one company we had many vCenters all run in the production environment for the other enviroments (not nested but same idea). The vCenter really is a control plane for the underlying compute layer where the VMs will exist and they are seperated. Sure you might lose all your visability into your environment if you lose your vCenter but you can always answer honestly that there will be no impact to the running workloads when asked in CAB. Logically then next step is to add the host to the vCenter.

![Empty vCenter image]({{ site.url }}/images/deploy-vcenter-7.JPG)

Whenever we do this we automate it and so I am enjoying the nuts and bolts feels of having to add this host myself, but it trust me you never want to have to do this for racks and racks of hardware. Maybe this is my appreciation for a handcrafted artifact when I know full well that our society relies on the success of mass production to sustain our world of abundance.

![Adding the host image]({{ site.url }}/images/add-host-to-vc-2.JPG)
![NUC Host in vCenter image]({{ site.url }}/images/add-host-to-vc-3.JPG)

Ohh now it is looking far more familiar, this is the view point I've spend way too much of my career. Not entirely sure what I need to do next, I clearly have some patching ahead of me. Ooh maybe I can play with the new Lifecycle Management features of vSphere 7. From what I saw at VMworld this is finally bringing all the pieces together and automated.

Thanks for reading.
Conor