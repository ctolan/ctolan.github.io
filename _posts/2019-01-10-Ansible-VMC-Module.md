---
layout: post
title:  "Ansible VMC Module"
date:   2019-01-10 09:56:31 +0100
tags: VMware Ansible
---

For the past week plus I've been developing a custom module for Ansible. Wait I should back up a bit. We are looking at using VMware VMC on AWS an amazingly promising service were VMware partnered with AWS to manage the underlying hardware for a managed vSphere environment as a service. They manage the hosts, they stand up the vCenter and you use it as a service - pay for what you need as long as you need it.

The upside of this if it works out is fantastic, no more dealing with host upgrades or capacity planning headaches. You can start with 3 hosts today and scale to 32 as needed. For a significant number of companies 32 hosts is more than they need, we'll need more.... the joy of scale.

Right where was I? Yes, enter ansible. As excited as I am about VMC, and impressed as I am by how they can create an SDDC environment on bare metal in two hours. I am still jealous of my colleagues who work in AWS and can save their configuration as code (cloudformation templates) and just stamp out identical copies of environments fully configured and ready to go. VMC will probably get there too, but right now after you get your SDDC environment you still need to go in and configure a number of things. What I am looking at is how to use a configuration management tool like Ansible to capture the configuration as code and splat it on top once stood up. We'd ideally put all this into a pipeline and give the power to create and configure a fresh out of the box environment to the business to use as they wish.

We're not quite there yet but working on it. Everyone gets quite excited when you talk about IaC and Config Management because of the clear benefits of having every configuration as code and less prone to human error, hence the rise of Ansible and Chef etc. But getting there is a task all in itself. People get excited about implementing Ansible because someone else has probably done the heavy lifting for you and you can pull down excellent playbooks that probable do most of what you need. Well this isn't true in my area, there is just enough for managing ESX hosts and vCenters and nothing yet for VMC. That is fine it is brand new, so let’s create it I guess. We are working with the APIs for VMC to create and manage SDDCs, the APIs are very good, built with Swagger from what I can tell.

Working with Ansible is a leap into Python for my team and we are a little hesitant because we are far more comfortable and advanced with PowerShell. Yet we embrace the challenge as everyone needs to know multiple languages these days anyway. I started my adventure by following and working through this really good [Ansible customer module blog](https://blog.toast38coza.me/custom-ansible-module-hello-world/). I worked through the hello-world example and then went on to great some Get API calls and then on to some POSTs. In the end of my little adventure I’ve a MVP module that takes in a definition of an SDDC in my Playbook and when runs will check to see if it exists on out in my Org and if not create it. If it finds the name exists it does nothing. The next step should we continue would be to add more parameters to the SDDC definition and then validate them if the SDDC exists. 

I have really enjoyed the project, it was an innovation sprint, I learned a lot about Python and Ansible. I’m still not sold on moving our whole team over to Ansible, we have all the above functionality written in PowerShell already. I ported over a couple of our existing functions from PowerShell to Python. Part of me wants to pursue the project with the intention of contributing it back to the community, but we could as easily do that in PowerShell and due to PowerCLI most VMware admins are PowerShell people…

Time will tell, I might take it on as a personal project outside of work just to get it started for others in our situation. 

Thanks for reading.