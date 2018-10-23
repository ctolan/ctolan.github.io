---
layout: post
title:  "Jeykll Tags In GitHub Pages"
date:   2018-10-22 09:56:31 +0100
tags: Jeykll-blog
---

Woop! I finally got tags working for my blog. The GitHub pages flavour of Jeykll is a special one so not all you read on the internet works out. I think I was following and backing out fourth or fifth blog before I struck on one I was sure should work. [Long Qian](http://longqian.me/2017/02/09/github-jekyll-tag/) has a good walk through of how to set everything up. My setup didn’t exactly match his, but his obvious successfully [working site](http://longqian.me/tag/github-page/) running right out of [his public repo](https://github.com/qian256/qian256.github.io) kind of smacked me in the face. It is as I say, _if you don’t know something it is your fault_, because all the information is out there. 

We are honestly at the pinnacle of humanity right now, anything you want to find is out there to be found. So with that taunting me I dug into his files and compared to my own until I finally got it all working. Bit by bit I worked it out, first I set up a sample page for just one tag. The links were being correctly created on the pages for /tag/tagname but they resolved to a 404 error page.

Turned out the tag folder had been created nested inside my “includes” folder, so I fixed that. That got the first tag working, so I’m close. I then ran Long’s python [tag generation script](https://github.com/qian256/qian256.github.io/blob/master/tag_generator.py) to generate stub pages for the rest of the tags. When I did I noticed that my format of tags was incorrect, it was a hangover from a tag blog that I’d followed. My tags were in an array format between square brackets so some showed up as *[PowerShell* which is wrong.

Nothing to do but fix them all, and while I’m at it I created tags for the rest of my posts. 

![Python Tag Generation Image]({{ site.url }}/images/tag-gen-script.PNG)

Here I am up way past my bed time, maybe sometime I’ll write about what I’ve learned about the importance of sleep but now now. 

Thanks for reading.
Conor