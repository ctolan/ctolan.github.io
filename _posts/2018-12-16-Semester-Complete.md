---
layout: post
title:  "SSL Cert Azure Web Apps"
date:   2018-11-29 09:56:31 +0100
tags: Azure DevOps MSc Certbot
---

In this post I will show you how I used LetsEncrypt to create an SSL cert which I was able to then apply to my Azure Web App. This meant I was able to use my custom domain name with https without the security warning caused by the wildcard Azure cert not matching my domain.


PS C:\Users\ctola> docker run -it --rm --name certbot -v "C:/etc/letsencrypt:/etc/letsencrypt"-v "C:/var/lib/letsencrypt:/var/lib/letsencrypt" certbot/certbot certonly --manual --preferred-challeng
es dns

https://www.ibm.com/support/knowledgecenter/en/SSPH29_9.0.1/com.ibm.help.common.infocenter.aps/t_ConvertthepfxCertificatetopemFormat068.html

https://rominirani.com/docker-on-windows-mounting-host-directories-d96f3f056a2c

https://certbot.eff.org/docs/using.html#where-are-my-certificates

https://hub.docker.com/r/certbot/certbot/

https://certbot.eff.org/docs/install.html#running-with-docker

https://certbot.eff.org/docs/using.html#manual