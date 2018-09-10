---
layout: post
title:  "Hey Google, put up the blinds!"
---

So what happens in your house when you say "Hey Google, put up the blinds!"

In my house a complicated series of events and triggers tell the three roller binds roll up to let in the light. 

Check out a short video i took <a href="https://youtu.be/gsLj6woppl0"> here on YouTube</a>
<iframe width="726" height="408" src="https://www.youtube.com/embed/gsLj6woppl0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

So what exactly happens?

First my Google Home recognises that I've used a phrase which is registered to call out to an Applet I setup on <a href="https://ifttt.com"> If This Then That</a>. 

![IFTTT applet image]({{ site.url }}/images/IFTTT-applet-1.png)

The Applet when triggered has a Webhook that POSTs a specific body string to the <a href="https://www.home-assistant.io">Home Assistant</a> webservice via <a href="https://www.duckdns.org/">DuckDNS</a>. Home Assistant is running on a rasberryPi, specifically the Hass.io build which makes it super easy to setup and keep updated.

Home Assistant is at the centre of my home automation setup, it is a great platform with a lot of cool integration right out of the box and it's free. 

Hardware wise I already had the powered blinds but they were manual, so i purchased IR remote switches on <a href="https://www.aliexpress.com/">Aliexpress</a> and installed them in place of the three manual switches. We are almost finished, there is one last piece to this the <a href="http://www.ibroadlink.com/rmPro/">Broadlink RM Pro</a> which is a trainable universal remote which can connect to Home Assistant. So I trained the IR remotes for blind switches into the RM Pro, and then I can trigger it remotely from Home Assistant.

All the pieces are now in place, the blinds are controlled by IR wall switches, which has been trained into the RM Pro, which can be activated from Home Assistant, which accept webhooks from IFTTT, which can connect to Google Home for custom voice commands. That is it for this post, i intend to delve into each part of this setup and do a how to that you can follow along to. It does get complicated in some places and yes you do need specific equipment to pull this off, but total cost was a lot less than some customer setup from any home automation professional.

Enjoy your weekend.
Conor
