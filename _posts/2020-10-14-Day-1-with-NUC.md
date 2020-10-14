---
layout: post
title:  "Day 1 with NUC"
date:   2020-10-14 09:56:31 +0100
tags: HomeLab
---

So yay, my NUC arrived, it is tiny and I'm really happy with how quiet and tidy it is. It'll happily sit on a shelf out of the way. I've worked with ESXi for many years now but i rarely get this hands on with hardware or do initial standup of enviroments. So this is a project that will fill in some gaps for me, I really hope I know what I am doing or it'll be embarrassing.
![Installing ESXi 7.0 image]({{ site.url }}/images/20201013_202925.jpg)

I installed a single 32GB stick of Crucial DDR4 ram, there are two slots in the NUC so if this project takes off I can add a second. While it states support for only 32GB RAM I have seen blogs which have been successful with 64GB. For storage I went with a 500G Samsung 970 EVO NVME M.2 SSD which should be enough for a few VMs, I wanted to keep costs reasonale. I think I'd rather have more NUCs than bigger NUCs, scale out not up and all that. I mean look at the size of this thing, that's an Amazon Echo for scale.

![NUC scale image]({{ site.url }}/images/20201013_203128.jpg)

I loosley followed this blog [Virten.Net](https://www.virten.net/2020/03/esxi-on-8th-gen-intel-nuc-coffee-lake-bean-canyon/) for how to get ESXi onto a 32GB USB stick. The USB key can be used as the destination for the installation too, so it is worth getting a decent one. That's all the hardware, I borrowed a keyboard and monitor connection from my office setup and booted up the little server.

The installation could not have gone smother, everything worked out of the box; next .. next .. next .. done. This is why I got a NUC the hardware is compatible so there is no messing with hacks or missing drivers. That seemed too easy - it booted up into ESXi and recieved an IP by DHCP. 

![ESXi 7.0 Success image]({{ site.url }}/images/20201013_204342.jpg)

Hmm what is this .... I cannot get to the host over HTTPS. Grr it was bitdefender blocking it for having an invalid cert. I'm in, I can manage the host direcrly from my laptop now. So i disconnect the keyboard and monitor relocate it to the shelf. Next steps is to vCenter installed and running, wish I hadn't wasted my one year VMware Advantage which I won at a VMUG. I didn't have the time or hardware then due to finishing my MSc. I'll figure something out, or I'll get really good at redeploying after the trail license expires.

Thanks for reading.
Conor