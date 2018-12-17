---
layout: post
title:  "Ansible On Windows Getting Started"
date:   2018-12-11 09:56:31 +0100
tags: Ansible Windows
---

Configuration management is going to be a major focus for us next year, we are currently weighing up Ansible versus our own developed scripts in PowerShell. PowerShell was my first choice, but Ansible seems to be worth investigating. There are a fair number of modules for VMware/vSphere out there already and we need to see if they meet our needs. The other option is to use PowerCli and to target the settings we care about. Since Ansible was designed to get and set configuration items it will be interesting to compare whether the learning curve is justified by the pre-existing art or complicated by forcing us into the mold.

First hurdle is getting ansible working on my Windows 10 laptop. I started with ambitions of running it within a container where I could setup all the tools etc but so far, I have run into road block after road block with containers. I spent longer than I expected finding a prebuild container with an up to date version of ansible installed. Then once I did, it didn’t have another module that I needed for the VMware modules called [PyVmomi](https://docs.ansible.com/ansible/latest/vmware/vmware_concepts.html#pyvmomi). I will keep at it for a while more, but my fall back has been to install Cygwin. This has worked well so far but neither great, the consoles don’t behave as nicely as I’d like, key input, copy and paste are a bit fiddly. But it works so I’ve been able to get started.