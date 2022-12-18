---
layout: post
title:  "Terraform Connected to GCP"
date:   2022-11-20 09:56:31 +0100
tags: GCP
---

With Terraform connecting to my GCP account I am able to start focusing on the infrastructure as code part of this project and less on the technical connectivity and setup which have been the focus of the previous posts. ![Gcloud Init 1]({{ site.url }}/images/Cloud-foundation-fabric-1.png)

What am I going to deploy? This is a question I have played around with quite a lot, and I think I have a good answer now. Previously I have thought about deploying some sort of app like an example app deployed in a container with all the pipeline bells and whistles that make it a cloud native app. These are quite common out there on the internet and usually come from software engineers who don't really take the infrastructure as seriously. Yet my experience really is in the infrastructure and not the app side of things. I don't really care about what application was going to be running and then those projects ran aground because it was not as interesting to me.

So what will I do differently this time, I am aware I started this series of posts without actually going into it. Well now is the time.

I have decided to deploy a mock enterprise datacenter using the [GCP Cloud Foundation Fabric](https://github.com/GoogleCloudPlatform/cloud-foundation-fabric). This will give me a fast way to stand up some cool infrastructure and to explore topics that are current and interesting to me. GCP is still a relative newcomer but has scored some top tier [customers](https://cloud.google.com/customers) as enterprises try to balance out their cloud spend and not be totally beholden to AWS.

So let me start now with the VPC Terraform module - for now right out of the documented examples as I don't have a specific design in mind at this time.

![VPC module config 1]({{ site.url }}/images/VPC-module-config-1.png)

Depending on your familiarity with Terraform, you may spot the source points to `github.com` directly, in a corporate environment you would fork the code into a local repo. This also allows you to make local copy changes where necessary. At this point I am not referencing a version tag, I am taking the latest. Ideally you will specify the specific version of the module which you have tested. I'll mature this config in time, but this is ok for now.

I have also improved the Terraform by moving some values into variables.

![Terraform variables 1]({{ site.url }}/images/Terraform-variables-1.png)

Variables make the code more reusable, I can define the project name in one location and then easily reference from now on as var.project. In each deployment folder I can then declare what variable may be different between folders such as the region or environment definition [prod] vs [nprd].

![Terraform variables 2]({{ site.url }}/images/Terraform-variables-2.png)

Here we also see the use of a terraform.tfvars file, this is an automatically loaded variables file. In contrast to a manually invoked variables file that could be called at run time on the command line. 

```
terraform plan -var=”env=prod” 
or 
terraform plan -var=”env=nprd”
```


```
terraform plan -var-file=”prod.tfvars” 
vs 
terraform plan -var-file=”nprd.tfvars”
```

It all depends on how different you environments are, but you get the idea you can keep the code identical between environments and with switches in the code have different outcomes. In the variables.tf file you can see where I commented out the default value once I moved them into the `terraform.tfvars` file.


![Terraform plan]({{ site.url }}/images/Terraform-plan-1.png)

I run `Terraform plan` command and like the look of it, one VPC and two subnets as expected. So run `Terraform apply` and answer 'yes'.

![GCP API disabled]({{ site.url }}/images/GCP-API-disabled.png)

Then `Terraform apply` throws this error - nothing big just I really am starting from scratch so the API has not been enabled. I followed the link and enabled my billing account. Redo the `terraform apply` and it works.

![GCP API disabled]({{ site.url }}/images/Terraform-apply-1.png)

So that covered a couple of small technical things but we are also making progress. With a network we can move onto deploying VMs next. 

Thanks for reading.

Conor