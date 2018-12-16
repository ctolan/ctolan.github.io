---
layout: post
title:  "LetsEncrypt SSL Cert Azure Web Apps"
date:   2018-11-29 09:56:31 +0100
tags: Azure DevOps MSc Certbot
---

In this post I will show you how I used LetsEncrypt to create an SSL cert which I was able to then apply to my Azure Web App. This meant I was able to use my custom domain name with https without the security warning caused by the wildcard Azure cert not matching my domain.

I googled and saw that someone had implemented LetsEncrypt as an automated task for Azure Pipeline (or VSTS) but when I looked for that task in Azure DevOps it is no longer there. Maybe they want to push you to purchase one from them? I don't know.

Either way I had enough to lead me to believe it was possible to get a cert from LetsEncrypt and to manually upload it myself to Azure.

![Certbot System Requirements image]({{ site.url }}/images/SSL-Azure-config-2.PNG)

Working back, to add an SSL cert to my custom domain, I need to bind it. To Bind it I need to have one available. To have one available I need to upload it. To upload it I need to have one!

I found [this blog](https://www.hanselman.com/blog/SecuringAnAzureAppServiceWebsiteUnderSSLInMinutesWithLetsEncrypt.aspx) where Scott Hanselman is using the Web App Site Extension. This looks like the way to go since it will automatically update the certs. I do not need the cert for years as my app is only for a project this semester so I will get the cert manually and upload it so i can get back to work on the report.

I'm going to do this manually and not from the webserver itself so according to the [Certbot documentation](https://certbot.eff.org/docs/using.html#manual)
I need to use something like this

```cmd
Certbot certonly --manual 
```

But wait - I need to get certbot, after looking at the options available to me on my Windows laptop:

![Certbot System Requirements image]({{ site.url }}/images/Certbot-System-Requirements-1.PNG)

[I opted to use Docker](https://certbot.eff.org/docs/install.html#running-with-docker). If you've never mapped the container volume to your laptop disks [check this out](https://rominirani.com/docker-on-windows-mounting-host-directories-d96f3f056a2c). The container needs a way to write out the keys to somewhere accessible to you after the container is shut down, this is the easiest way. Here is [the container](https://hub.docker.com/r/certbot/certbot/)

After a couple of false starts I arrived at my final certbot invocation. In this I call Docker with an interactive terminal connected (-it), and (--rm) to remove the stopped container after execution. I call the container certbot (--name) and mount the volumes C:/etc/letsencrypt to /etc/letsencrypt and C:/var/lib/letsencrypt to /var/lib/letsencrypt. I had to create these folders locally first and they do not need to be in this path specifically. I use the manual switch and certonly command that I read about previously, but also I specify that my preferred validation of domain ownership is via DNS.

```powershell
PS C:\Users\ctola> docker run -it --rm --name certbot -v "C:/etc/letsencrypt:/etc/letsencrypt"-v "C:/var/lib/letsencrypt:/var/lib/letsencrypt" certbot/certbot certonly --manual --preferred-challeng
es dns
```

In one of my first attempts it asked me to make available a challenge file on the webserver but with Azure Web App services this seemed more complicated than DNS validation.

Once run you will see the following after you supply your domain and email address.

![Certbot DNS challenge image]({{ site.url }}/images/SSL-cert-validate-1.PNG)

This is asking that I prove my ownership of bp.conortolan.com by placing the text into DNS, it is assumed that if you can do that then you are likely the owner of the domain.

In GoDaddy I created the following TXT record on the subdomain.

![Create DNS TXT record image]({{ site.url }}/images/SSL-DNS-setup-1.PNG)

I tested it at the cmd line to be sure.

![Verify DNS TXT record image]({{ site.url }}/images/SSL-DNS-validate-1.PNG)

And success.

![Certbot SSL Cert created image]({{ site.url }}/images/SSL-cert-created-1.PNG)

After a quick look at [where are my certs](https://certbot.eff.org/docs/using.html#where-are-my-certificates) I have what I've been after, but not in the format compatible with Azure... of course not.

So back to Google and a quick read of [this article on converting to pfx](https://www.ibm.com/support/knowledgecenter/en/SSPH29_9.0.1/com.ibm.help.common.infocenter.aps/t_ConvertthepfxCertificatetopemFormat068.html) and I was away again.

![SSL Cert Convert to .pfx image]({{ site.url }}/images/SSL-cert-convert-1.PNG)

In my Windows Subsystem for Linux (WSL) I use openssl to export the certificate PEM file as a p12 formatted certificate as per the linked article. In the screenshot I used the wrong file extension, I redid it again with .pfx and that was successfully imported into Azure.

Once I had the certificate uploaded to Azure it was easy to bind it to the custom domain.

![SSL Cert Convert to .pfx image]({{ site.url }}/images/SSL-Azure-config-1.PNG)

That's it, with that I now have my own (free) SSL certificate on my custom domain in Azure. I flipped the switch for HTTPs only and will leave it at that for now, knowing that if I keep this site up after my project is finished I should really setup automatic renewal of the certificate. That will be for another day, we were not even asked to add SSL to our projects I am just showing off.

Thanks for reading I hope this helps.

Conor.