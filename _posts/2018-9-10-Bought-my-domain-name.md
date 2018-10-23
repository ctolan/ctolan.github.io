---
layout: post
title:  "I Bought My Domain Name."
date:   2018-09-10 14:56:31 +0100
tags: Jeykll-blog
---

Today I took the advice of Gary Vaynerchuk and bought my domain name. This is a quick write up on how it went applying it to my GitHub Pages blog. I started out on GoDaddy and bought the domain name via PayPal. The two year order seemed reasonably priced at about $10 a year (side note why does conordean.com cost $899 because he’s an Irish rugby player), with the domain mine first thing I did was setup forwarding to try it out. 
![GoDayy Forward image]({{ site.url }}/images/GoDaddyForward-min.PNG)

This worked but the domain of the site does not change from ctolan.github.io, as you may expect is a forward from conortolan.com to ctolan.github.io. After reading help pages on how to setup an A record I headed to the GoDaddy “Manage DNS” section and added the four required IPs.

![GoDayy A Records image]({{ site.url }}/images/GoDaddyARecords.PNG)

<a href="https://help.github.com/articles/setting-up-an-apex-domain/">"https://help.github.com/articles/setting-up-an-apex-domain"</a> 

Next I added the custom domain on GitHub by going to the settings and saved my domain.
I cancelled the forwarding too by the way, but not before experiencing the never ending loop of conortolan.com forwarding to ctolan.github.io which tried to resolve conortolan.com as the site name.

<a href="https://help.github.com/articles/adding-or-removing-a-custom-domain-for-your-github-pages-site/">"https://help.github.com/articles/adding-or-removing-a-custom-domain-for-your-github-pages-site/"</a> 

Now my site is up and running at conortolan.com as you can see, but I’ve not yet got the HTTPS working. There is a note that it can take 24 hours, so hopefully that’s all it is.

![GitHub HTTPS image]({{ site.url }}/images/GitHubHTTPS.PNG)

Other links I looked at while setting this up.

<a href="https://help.github.com/articles/quick-start-setting-up-a-custom-domain/">"https://help.github.com/articles/quick-start-setting-up-a-custom-domain/"</a>
<a href="https://blog.github.com/2018-05-01-github-pages-custom-domains-https/">"https://blog.github.com/2018-05-01-github-pages-custom-domains-https/"</a>
