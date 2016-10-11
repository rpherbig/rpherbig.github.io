---
title: What We've Got Here is a Failure to Authenticate
layout: post
---

In [the previous post](TODO), we set up server-side rules to redirect HTTP traffic to HTTPS. Using HTTPS ensures that the client and server are communicating securely and that no one is [intercepting the traffic](https://en.wikipedia.org/wiki/Man-in-the-middle_attack). An example of this redirection is in row 1:

![](/images/URL_Redirects.png)

But there's still a problem: the browser is making that initial request over HTTP. That request is still vulnerable and a malicious entity could prevent the redirect to HTTPS.

## HSTS and you

[HTTP Strict Transport Security](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security) (HSTS) is a security policy which indicates that your site should always be accessed over HTTPS. Enabling it means that now your browser won't make that initial connection over HTTP. Instead it will internally redirect itself to the location from before, which uses HTTPS.

![](/images/HSTS_Redirect.png)

Luckily for us, Cloudflare makes it easy. On the [Crypto configuration page](https://www.cloudflare.com/a/crypto/), there is a HSTS setting. Before you can enable HSTS, there's a bunch of warning text to read and acknowledge, and for good reason. Since you are telling browsers to always use HTTPS, if HTTPS somehow becomes disabled or invalid on your site, users will not be able to view it. The HSTS setting has a 'max-age' which indicates for how long it is applicable. That means your site may be completely inaccessible to users for that long.

Don't let the warnings scare you. As long as you're aware of the implications, HSTS is a good security feature. Test your HTTPS connection thoroughly first. Then when you are confident it is working, set 'max-age' to a small value (ideally 1 day or so; but if you're using Cloudflare you are stuck with 1 month). Continue testing and gradually increase 'max-age'. Also be aware of [browser compatibility](http://caniuse.com/#feat=stricttransportsecurity).

To disable HSTS, carefully reverse the process. Turn off the HSTS policy, but keep supporting HTTPS until 'max-age' has elapsed. Then you can disable HTTPS.

But there's still a (smaller) problem: HSTS only prevents the browser from making subsequent requests over HTTP. The browser is still making that initial request over HTTP, which is a potential vulnerability.

## Preloading to the rescue

Many smart people have thought this over and decided that browsers should have a list of sites which support HSTS preloaded when they ship. If you visit a site which is in this list, your browser doesn't even make that first call over HTTP - it already knows to use HTTPS.

To submit your site for inclusion in the preload list, you must redirect HTTP traffic to HTTPS and include the HSTS header. The max-age must be at least eighteen weeks, use the includeSubDomains option, and use the preload option. The steps on these two blog posts, plus Cloudflare's defaults where not specified, meet those requirements. Now it's just a matter of visiting the Chromium [HSTS preload submission app](https://hstspreload.appspot.com/).
