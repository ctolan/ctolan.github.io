---
layout: post
title:  "Starting To Learn SEO"
date:   2018-10-18 09:56:31 +0100
author:
  twitter: ConorT
tags: SEO Learning
---

I had some idea, but really no idea just how complex Search Engine Optimisation (SEO) had gotten. I have added Google Analytics to this site for insight and experience. I’m only starting out so as expected I’ve next to not readers, but with my PowerShell Lambda posts coming within a month of their publication I thought maybe I’d be higher in the organic ranking for the specific keywords AWS Lambda PowerShell. Boy was I wrong. 

Not even close to the front page, I’m on with that, it is not why I’m doing this, but it got me wondering why.
I dug a little bit and started to wonder if my site was SEO optimised or not. I did have the [basic SEO enabled](https://blog.github.com/2016-05-10-better-discoverability-for-github-pages-sites/), but reading a couple of [optimise your Jekyll](https://blog.webjeda.com/optimize-jekyll-seo/) blog posts I found [posts about speed](https://blog.webjeda.com/jekyll-speed/) which linked out to [GTmetrix](https://gtmetrix.com/).

This site was a real eye opener to the sheer complexity of detail that goes into SEO. I had under estimated the impact of not resizing my images and the tests were quick to point out that my 3mb photo could be resized to 1400x800 and optimized to save 82% file size. It is detailed and specific, and highlighted the need for alt text on my images, which mostly I had. It though was able to see that my avatar did not have alt text. I ventured into my layouts and found the image src and added one, I added site.name as that’ll be me and it is better than hard coding it.

```html
<header class="masthead clearfix">
  <a href="{{ site.baseurl }}/" class="site-avatar"><img src="{{ site.avatar }}" alt="{{ site.name }}"/></a>
```

Here is a scan of an optimised page, not a lot left I can optimise. I guess I can scale down my avatar photo….

![Pretty good GTmetrix report Image]({{ site.url }}/images/GTmetrix-report-1.PNG)

On the waterfall tab you see the timeline of the items downloads for your page. My favicon was getting a 404, I’ve since fixed that. It was not an out of the box setting in Jeykll so it may never have happened if it was not for seeing this test.

![GTmetrix waterfall tab Image]({{ site.url }}/images/GTmetrix-report-2.PNG)

One thing that struck me quite quickly is that this is not a quick process, it is not a case of flipping a switch and your entire blog is SEO’d. This will take time, time of resize and optimise my images, time to hunt down CSS for above and below the fold and time to tweak my URL choices, all for better organic search scores.
Check out my home page, after more than one pass at optimising it.

![GTmetrix waterfall tab Image]({{ site.url }}/images/GTmetrix-report-3.PNG)

Still not pretty.
What was really insightful though was how bad the Disqus comments add on was for my page. I had tracking pixels and added to the page load time, all in all I decided to just remove it. It’ll be a project for another time to find a less intrusive comments section.
Maybe this is over thinking it and I should return to not caring for now, not until I’ve a lot more free time than I do right now.