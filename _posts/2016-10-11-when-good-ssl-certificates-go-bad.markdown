---
title: When Good SSL Certificates Go Bad
layout: post
---

I recently [wrote a blog post](https://www.rpherbig.com/2016/09/30/a-lot-can-happen-in-a-year.html) after a long period of inactivity and I got some feedback. The most common response was "you blog?" - but the second most common response was "hey, [your SSL certificate is bad](https://www.youtube.com/watch?v=jG2KMkQLZmI)". This was rather unexpected since I use GitHub Pages specifically to avoid having to think about that sort of thing.

Sure enough, when I went to www.rpherbig.com in Chrome I got an Unsafe Site warning:
![](/images/UnsafeSiteWarning.png)

That's no way to greet people visiting my blog. Proceeding to the site gives a bit more information:
![](/images/Broken_HTTPS.png)

It turns out that this is a known problem when using GitHub Pages and a custom domain. In fact, it's been a problem since at least 2014. I'm not sure how it took me this long to notice, but enough is enough - it's time to do something about this.

## You only need [one piece of flare](https://www.youtube.com/watch?v=KJtrLKGZZFg)

Enter Cloudflare, stage right. Cloudflare's product sits between the end user (you, reading this blog post) and the content server (in this case, GitHub Pages). Cloudflare offers a [whole lot of services](https://www.cloudflare.com/) - among them making it easy to configure SSL (image courtesy of [CloudFlare's blog post on the introduction of strict SSL](https://blog.cloudflare.com/introducing-strict-ssl-protecting-against-a-man-in-the-middle-attack-on-origin-traffic/)):
![](/images/Cloudflare_Full_SSL.png)

The signup process is painless and straightforward. I won't detail the steps I took here since I used the defaults. Do note, it took the better part of a day for my SSL certificate to be authorized, and a bit longer yet for the name server (DNS) changes to propagate and take effect. The next day I was back in business:
![](/images/Valid_HTTPS.png)

## Not so fast...

All of our hard work only matters if the visitor is using HTTPS, so let's force its use. GitHub Pages allows you to [enforce HTTPS](https://help.github.com/articles/securing-your-github-pages-site-with-https/), but only if you are using the `github.io` domain.

For a custom domain, it's a bit trickier. You will need to create up to three Page Rules in Cloudflare (depending on if you're using a `www` subdomain like I am):

<table border="1">
    <tr>
        <th>URL matches</th>
        <th>Setting</th>
    </tr>
    <tr>
        <td>http://rpherbig.com/*</td>
        <td>Always Use HTTPS</td>
    </tr>
    <tr>
        <td>http://www.rpherbig.com/*</td>
        <td>Always Use HTTPS</td>
    </tr>
    <tr>
        <td>https://rpherbig.com/*</td>
        <td>Forwarding URL (301 - Permanent Redirect): https://www.rpherbig.com/$1</td>
    </tr>
</table>

Once you have the Page Rules in place, I highly recommend testing them by visiting each of the URLs to ensure they redirect properly. In this example, you would test http://rpherbig.com, http://www.rpherbig.com, and https://rpherbig.com - and expect them all to redirect to https://www.rpherbig.com.

![](/images/URL_Redirects.png)

Here you can see my test for http://rpherbig.com. Cloudflare redirected us to https://rpherbig.com (row 1). Then https://rpherbig.com was redirected to https://www.rpherbig.com (row 2). Then the final URL of https://www.rpherbig.com was loaded (row 3).

It's important for the security of your site that these Page Rules be set up correctly so that the redirects happen in the proper order. If https://rpherbig.com redirects to http://www.rpherbig.com, you're in trouble, even if you eventually end back up on HTTPS.
