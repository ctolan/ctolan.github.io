---
layout: post
title:  "Connecting Terraform to GCP"
date:   2022-11-14 09:56:31 +0100
tags: GCP
---

Next thing I want to get working is `Terraform Plan` against my GCP project. I quickly swapped out of my blog volume to a `Code` folder where I will keep my `.tf` files.


```
  --volume="C:\Users\ctola\Documents\Blog":"/blog" 
```
to
```
  --volume="C:\Users\ctola\Documents\Code":"/code" 
```

I will create a folder for my data-center deployment code. I will distinguish between two types of code, deployment and configuration. 
- _Deployment code_ is specific to resource deployment, the regions, resource names, specific IPs for VPNs in that region.
- _Configuration code_, is the TF module code which will do the configuration as defined by the deployment code.

You should only have one copy of the configuration code and possibly many copies of the deployment code, each slightly different maybe for different regions or different uses such as Development versus Production.

If I jump in and get ahead of myself and run Terraform plan now with only a skeleton configuration we will see the immediate issue which we need to address. Copying straight from the GCP Terraform documentation [here](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/getting_started), I will populate my project name in the provider block and I'll accept the default region configuration. Just as an aside the US Central is a low carbon footprint region, apparently, so its a good default.

![TF Initial 1]({{ site.url }}/images/Terraform-main-tf-initial-1.png)

Below the `provider` block I copy paste a compute instance `resource` block. I will not configure this at all now because I do not expect it to actually work.

![TF Plan Error 1]({{ site.url }}/images/Terraform-plan-error-1.png)

With only these two blocks defined you can run `Terraform init` and `Terraform plan`. This is not a blog on how to use Terraform but init initialises the folder as a workspace and checks the files for a Terraform configuration, if access to the required modules is not avaialble this is where you will get an error. In my case, there is no issue initialising, but when Terraform tries to connect to GCP there is a permissions error. This makes sense I have not done any authentication yet.

```
Error: Attempted to load application default credentials since neither `credentials` nor `access_token` was set in the provider block.  No credentials loaded. To use your gcloud credentials, run 'gcloud auth application-default login'.
```

To use gcloud credentials run 'gcloud auth application-default login'. Ok so we have not yet added `gcloud` to the container so now is the time.

I will install gcloud cli as per instructions [here](https://cloud.google.com/sdk/docs/install#linux), I will copy the commands into the Dockerfile in a new block for readability. Actually, gcloud cli need python, so that needs to be installed too. I'm copying from [here](https://computingforgeeks.com/install-latest-python-on-centos-linux/) for Python.

I know I go on about this often but this is why I use the container approach. Too many times have I wanted to share a tool or piece of automation with a colleague but the pre-requirements are missing and it takes way longer than it should. With a shared team container, you only have to do all this setup once, no issues with missing dependancies or incompatible versions. Yes it is more work if taken in isolation for a single simple task but most thinks I do are not single simple tasks and by dragging out this blog with every step I hope I am helping top make that clearer. It a complex house of cards build up bit by bit relying on all the bits below.

To run `gcloud auth` it means I need `glcoud cli`, but also I need Python 3.5-3.9 and for that in CentOS 7 I will need a compatible gcc complier, for that I am best off installing Linux "Development Tools" and so on. After installing Python, to install the gcloud cli it is handy to have `wget` and then `tar` to unpack it. I am aware that there are now redundant tools used in commands to do similar things. For example curl and wget or unzip and tar. Why not re-write the example command? Having both of these common tools in my container is going to be useful down the road, so I will add them now.

Right so after working through all that this is my current Dockerfile.

![Dockerfile 4]({{ site.url }}/images/Dockerfile-4.png)

I've added commands to get and remove the packages for Python 3.9 and GCloud Cli. I added some more yum package installs to facilitate it. I'll collapse them into a single line shortly as it saves on container layers but that's not important here and now.

![Dockerfile 4]({{ site.url }}/images/Dockerfile-build-1

After the successful build (no I didn't get it right the first time), then I can run `gcloud init` in my container. Yay.

Oops - crashed docker while relocating my laptop. I'll add a screenshot later.

Thanks for reading.

Conor