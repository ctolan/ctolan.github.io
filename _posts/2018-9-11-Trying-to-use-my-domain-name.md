---
layout: post
title:  "Trying to use My Domain Name."
date:   2018-09-11 14:56:31 +0100
---

Yesterday I bought my domain name conortolan.com and I played around with domain forwarding quite successfully. Sadly I have not been so successful with using setting the domain as my custom domain on GitHub. While I’ve gotten the basics working I am struggling a bit with HTTPS and mixed content. I am hoping that I just need to be patient and let the process happen with GitHub and LetsEncrpyt sorting it all out in the background as per the message below.
![GitHub HTTPS image]({{ site.url }}/images/GitHubHTTPS.PNG)

My prodding and poking has come to nothing but I also haven’t waited a full 24 hours without poking and prodding it.

I was also looking at the Themes for Jekyll, there is an option to add one on the GitHub pages setting page but it is not working. I think I should leave it to one change a time for now as I get to know the system and what is possible. For example the structure of the pages is familiar to what I learned when playing around with the MVC pages in Django: 
![Index.html image]({{ site.url }}/images/index.html.PNG)

What we get is a page dynamically created page by looping over each “post” in “site.posts”, it’s a simple loop where a new link to “post.url” and “post.title” is created along with a “post.excerpt”. Django had a CLI that let you get in and explore the properties of its objects, I bet this does too. Yet I love that I don’t have to. For me it means if I need to get in and make changes down the road it shouldn’t be too difficult to figure out.
