---
layout: post
title:  "Tear it down and start again"
date:   2018-09-11 14:56:31 +0100
---

The HTTPS and DNS forwarding is now working yet so I'm going to do what we always do in siturations like this. Tear it all down, go back to the start and do it again, but with the knowledge of what didn't work last time.

First i deleted the 4 A records in GoDaddy.com, i'm giving them 30min to clear as that was the TTL (time-to-live).
Next i removed the custom domain from the Settings page of the GitHub repo.

In 30 min i will more accuratly follow the steps layed out in the Quick Start.

<a href="https://help.github.com/articles/quick-start-setting-up-a-custom-domain/">https://help.github.com/articles/quick-start-setting-up-a-custom-domain/</a>

I completed the steps out of order by creating the A records before setting the Cusatom domain in the repo settings. I'd hoped i could remedy that by just removing and re-adding the customer domain but two days later and it is not working, so i'm learning my lesson and going back to the start.
