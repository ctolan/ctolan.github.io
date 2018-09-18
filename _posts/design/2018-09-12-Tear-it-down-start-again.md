---
layout: post
title:  "Tear it down and start again"
date:   2018-09-12 09:56:31 +0100
---

# Not yet working
The HTTPS and DNS forwarding are not working yet, so I'm going to do what we always do in situations like this tear it all down, go back and do it again. This time with knowledge I didn't have the first time.

First I deleted the 4 A records in GoDaddy.com, I’m giving them 30min to clear as that was the TTL (time-to-live).
Next I removed the custom domain from the Settings page of the GitHub repo.

In 30 min I will more accurately follow the steps laid out in the Quick Start.

<a href="https://help.github.com/articles/quick-start-setting-up-a-custom-domain/">https://help.github.com/articles/quick-start-setting-up-a-custom-domain/</a>

I completed the steps out of order by creating the A records before setting the Custom Domain in the repo settings. I'd hoped I could remedy that by just removing and re-adding the customer domain but two days later and it is not working, so I’m learning my lesson and going back to the start.

# And of course that worked!
So within less than an hour of actually re-doing it the Quick Start way it is working. One slight difference in the GoDaddy config is that I removed the "Parked" A record that may or may not have been problematic. It did show up when I ran dig against my domain.
