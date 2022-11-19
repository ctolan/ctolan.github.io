---
layout: post
title:  "Adding TFEnv to Container"
date:   2022-11-12 09:56:31 +0100
tags: GCP
---

Picking up from the end of the last post I needed to include my Git config inside my container so that I do not need to leave the container to use Git. I do this by mounting my .gitconfig file from my laptop into the container where it will be used while running in the container. This is how I get the right mix of disposability and persistence between my laptop and working container environment. 

```
docker run --rm /
  --volume="C:\Users\ctola\Documents\Blog":"/blog" /
  -it docker.io/library/mycontainer:local
```
to
```
docker run --rm /
  --volume="C:\Users\ctola\Documents\Blog":"/blog" /
  --volume="C:/Users/me/.gitconfig":"/root/.gitconfig" /
  -it docker.io/library/mycontainer:local
```

Again this is why I save this command, I don't want to get deep into a repo update and then realise I haven't go whatever setting configured and I need to go set it and lose my flow. This pattern can be use with other file configs too, and you do not need to mount an actual in use file, it could be a specific file that you place in a persistent location just for ease of use. You might have one .ssh config for one project and another in another folder. You would swap between them by changing the one mounted at run time.

Project 1
```
docker run --rm /
  --volume="C:\Users\ctola\Documents\Blog":"/blog" /
  --volume="C:/Users/me/configs/Project_1/.gitconfig":"/root/.gitconfig" /
  -it docker.io/library/mycontainer:local
```
Project 2
```
docker run --rm /
  --volume="C:\Users\ctola\Documents\Blog":"/blog" /
  --volume="C:/Users/me/configs/Project_2/.gitconfig":"/root/.gitconfig" /
  -it docker.io/library/mycontainer:local
```

Right with that working I want to get Terraform installed. I'm going to take the Dockerfile from yesterday and add some lines. [TFEnv](https://github.com/tfutils/tfenv), this tool allows quick and easy version switching and handles the installation.

![Dockerfile-2]({{ site.url }}/images/Dockerfile-2.png)

I added a blank line to create a block of lines dedicated to installing and configuring TF. Starting with a `ARG` line, think of this as a variable. In this variable I will specify the Terraform version number that I want to use, having this defined in one place and then used in a few makes it easier to change in the future. I got these commands straight from the Github linked above.

In the image you can see a commented line which i left in to make the following point. The off the shelf path for the bash profile didn't match the OS version I have chosen, so the first time I built the container it errored on line 15 because the `tfenv` binary was not in the path. Hence you can see that I put the full path to get it to build. I tried to source the profile but didn't work until I realised it was the wrong filename for the bash profile. I added the correct path and it is working now.

I will now remove the last `source` line and the commented out line. Wether I bother to replace the full path with a short path I dont know, maybe.

![Terraform-Version-1]({{ site.url }}/images/Terraform-version-1.png)

Bottom line Terraform is now installed in my container, in a way which makes up upgrading easy in the future.

Thanks for reading.

Conor