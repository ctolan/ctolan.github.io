---
layout: post
title:  "Updated Hassio via API"
date:   2018-09-16 09:56:31 +0100
---

That took too long! I have spent quite a bit of time today trying to fix my borken Home Assistant setup. It was not totally borken, but there was a bug in version 0.75 preventing me from accessing the /hassio page where i could then update to a non-buddy version. I found the <a href="https://github.com/home-assistant/home-assistant/issues/15816">issue page</a> with a quick Google but as I've mentined in my last post, I dont have a screen or keyboard attached to my Raspberry Pi. It sits in a cupboard. I tried to connect via SSH, and i spent time validating i had the SSH add-on, but when i SSH'd to the Pi IP, I didn't know the password. It wasn't the API password, it wasn't blank, honestly if i knew what it was this would be a sorter story.

So what is the next best thing to SSH - an API and Home Assistant has one (and a cli but that presumes you can connect). I dont think I had the API component even enabled, so I got that added into my configuration and I confirmed that the API was eventually working with Postman. For those who don't know it is a free too for working with API's - it's great.  