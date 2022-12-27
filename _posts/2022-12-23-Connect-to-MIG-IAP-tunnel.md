---
layout: post
title:  "Connect to MIG Over IAP tunnel"
date:   2022-12-23 09:56:31 +0100
tags: GCP
---

Hello, The most obvious thing to try to do next is to SSH to the VM, but I do not want to be able to connect to these VMs openly over the internet. So I will use Google's Identity Aware Proxy (IAP) to tunnel into the VMs without having to setup complicated VPN tunnels or opening firewalls to the internet. ![Add IAP Permission 1]({{ site.url }}/images/Terraform-Add-IAP-perms-1.png)

Ok, I know I just started writing this up, but it took me three days to get to the bottom of why it wasn't working. Classic d'uh moment.

Loosely I was following the steps as [laid out here in this article](https://medium.com/google-cloud/how-to-ssh-into-your-gce-machine-without-a-public-ip-4d78bd23309e), but I was going to do it completely in Terraform code. While it is clearly important to know how to enable service APIs via the UI, for Infrastructure As Code (IAC) you need to know how to do it with the code.

![Add IAP Permission 1]({{ site.url }}/images/Terraform-add-IAP-service-1.png)

I pulled together these few resource blocks on the first day, no big deal. Applied them with Terraform and expected everything to work like it does in work and like it said it would in the above linked article. Of course it did not work.

![IAP Self test 1]({{ site.url }}/images/IAP-SSH-self-test.png)

I ran the connectivity tests multiple times, I checked again that I had actually see that SSH was open to the whole world by default.

![Firewall Settings 1]({{ site.url }}/images/Firewall-settings-1.png)

Tried to use the SSH via web browser, all failed to connect. I went back and looked at the created resources and permissions in the TF code. I tried to google what other authentication method I might be using that we do not use in work, but I could not make any progress. I even spun up a fresh VM from a GCP template via the UI incase it was something wrong in my deployment changes from the previous post. In some way I'm glad I didn't find anything because I means I had followed these steps correctly, but in a more meaningful was I was frustrated that I was not working. That was until I looked again at the default firewall rule. I was going in there to confirm that it was an `allow` rule and maybe recreate the rule to prove I wasn't crazy. This is when I saw that the network was configured as `default`. This didn't mean anything much except I was not deploying my VMs to the `default` network and subnets. I had deployed my own network, so the firewall rules for the default network did not apply. I could not SSH because the firewall was not open. 

Whether or not now is a good time to write about importing existing resources such as the default network into your TF in order to destroy it, since it is not contained in your IAC, would be an interesting idea. But I'll leave this post here because it took me way longer than I expected to be able to SSH to my deployed VMs over the IAP tunnel, which once allowed to connect did so as expected, mostly.

![SSH Works Kinda 1]({{ site.url }}/images/SSH-works-kinda-1.png)

Thanks for reading.

Conor