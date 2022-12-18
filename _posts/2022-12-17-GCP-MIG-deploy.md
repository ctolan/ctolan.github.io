---
layout: post
title:  "GCP MIG deploy"
date:   2022-12-17 09:56:31 +0100
tags: GCP
---

Hello, so I'm thinking about what exactly to deploy, I have a few good ideas from recent work tasks but I would need to develop a few more bits of supporting infrastructure and services. So I am not sure what order to proceed. Today I'll start with deploying a managed instance group (MIG). If you know AWS you can think of this like an auto-scaling group. Basically it is a set of VMs that are managed as a group to provide highly available services. ![MIG Deployed 1]({{ site.url }}/images/GCP-Instance-Groups-1.png)

Sticking with the theme of this blog, I will deploy the example straight form GCP Cloud foundation fabric, the [Compute-MIG](https://github.com/GoogleCloudPlatform/cloud-foundation-fabric/tree/v19.0.0/modules/compute-mig) bundles a few bits of infrastructure together with minimal TF code and understanding to implement. This method gets you off the ground quickly while you learn the components which work together behind the abstraction.

![TF MIG Code 1]({{ site.url }}/images/Terraform-plan-2.png)

Here I have copied over the three Terraform resources from the [first example](https://github.com/GoogleCloudPlatform/cloud-foundation-fabric/tree/v19.0.0/modules/compute-mig#examples) of a MIG. I changes the source to be Github and not the relative path in the example. In a real enterprise you will point to your own corporate source control repository. I do not recommend using a local copy of their repo as a relative path. 

```
module "cos-nginx" {
  source = "./modules/cloud-config-container/nginx"
}
```
to
```
module "cos-nginx" {
  source = "github.com/GoogleCloudPlatform/cloud-foundation-fabric//modules/cloud-config-container/nginx"
}
```

I am actually really glad I came back to look at these examples again because I had missed or overlooked or more likely under appreciated the next example of [multiple versions](https://github.com/GoogleCloudPlatform/cloud-foundation-fabric/tree/v19.0.0/modules/compute-mig#multiple-versions), I am pretty sure this is something I have been looking for to complete a task at work. I'll cover this when I get to a point of implementing it and I should add a link when the post is created [TODO].

Oh yes, the other thing I changed here is the OS. I have been using Centos mostly so I replaced the boot image, will this work? I don't know. I hope so.

![TF plan error 2]({{ site.url }}/images/Terraform-plan-error-2.png)

Ok looks like there is more to update, I replaced the network and subnetwork references but I didn't get it right the firs time. I needed to reference one of the two subnets I created in my [last post](https://conortolan.com/Terraform-Connected-to-GCP/) 

![TF plan error 2]({{ site.url }}/images/Subnet-code-1.png)

This is the final state I came to after a bit or trial and error. I should probably extract the region into a variable, that would make it better too, but I understand that it is easier to read the code when there are not too many abstractions all at once.

![TF Apply 1]({{ site.url }}/images/Terraform-apply-2.png)

These three resources have been successfully applied to the project.

Thanks for reading.

Conor