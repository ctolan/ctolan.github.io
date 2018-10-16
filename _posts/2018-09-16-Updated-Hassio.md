---
layout: post
title:  "Updated Hassio via API"
date:   2018-09-16 09:56:31 +0100
---

That took too long! I have spent quite a bit of time today trying to fix my broken Home Assistant setup. It was not totally broken, but there was a bug in version 0.75 preventing me from accessing the Hassio page where i could then update to a non-buddy version. I found the issue page with a quick Google but as I've mentioned in my last post, I don’t have a screen or keyboard attached to my Raspberry Pi. It sits in a cupboard.

I tried to connect via SSH, and I spent time validating I had the SSH add-on, but when I SSH'd to the Pi IP, I didn't know the password.

It wasn't the API password, it wasn't blank, honestly if I knew what it was this would be a sorter story.
So what is the next best thing to SSH - an API and Home Assistant has one (and a cli but that presumes you can connect). I don’t think I had the API component even enabled, so I got that added into my configuration and I confirmed that the API was eventually working with Postman. 

For those who don't know it is a free too for working with API's - it's great.
To interact with the Hassio APIs first thing you will want to validate is that the API service is up and running. Reading <a href="https://github.com/home-assistant/hassio/blob/dev/API.md"> this API</a> page on GitHub there should be an endpoint that we can hit to get a Ping back.

 > Hass.io
 > 
 > GET /supervisor/ping
 >
 > This API call don't need a token.

I tried this for a while and I added a X-HASSIO-KEY header but I kept getting 404 errors. I couldn’t find anywhere that actually said for sure that the X-HASSIO-KEY was the same HTTP key/password that is set in my configuration.yml file. Either way I move away from this help document and on to <a href="https://developers.home-assistant.io/docs/en/external_api_rest.html">this one</a> which to be fair does seem more official, but does no mention updating Hassio Sad face.
I opened up the WSL to get CURL and I tried the first endpoint

```bash
curl -X GET -H "x-ha-access: YOUR_PASSWORD" -H "Content-Type: application/json" http://IP_ADDRESS:8123/ENDPOINT
```

> GET /api/
> 
> Returns a message if the API is up and running.
> 
>  {
>    "message": "API running."
>  }

So what does this look like:

```bash
curl -X GET -H "x-ha-access: MY_PASSWORD" -H "Content-Type: application/json" https://MyDNS.Duckdns.org/API`
```

To be fair to the documentation – once I got here it was all starting to drop into place. This worked and I got the API running response. I had successfully added API config and it was listening. 
I needed the https because I have configured https with Let’s Encrypt, you don’t if you have not. Look at how you connect to the Home Assistant dashboard and copy that.
In Postman it will look like this:
TO DO Postman Image.
I also tried the configuration endpoint just to be sure it wasn’t a fluke: 

```bash
curl -X GET -H "x-ha-access: MY_PASSWORD" -H "Content-Type: application/json" https://MyDNS.Duckdns.org/API/Config`
```

It wasn’t, it worked, so I have API access but do not know what command will initiate the Update of Hassio off of the broken version.

Eventually I found a hint in another [issue post](href="https://community.home-assistant.io/t/hass-io-not-running-after-upgrade/23980") that maybe something like `curl -X POST http://172.17.0.4/homeassistant/update` might work.

So I constructed the call in Postman, fired it off and waited.

```bash
curl -X GET -H "x-ha-access: MY_PASSWORD" -H "Content-Type: application/json" 
https://MyDNS.Duckdns.org/homeassistant/update`
```

First time it hung/failed to complete but the second time I got the successful response from Home Assistant.

I waited for the update to complete and refreshed the dashboard page and success I was updated to 77.3

