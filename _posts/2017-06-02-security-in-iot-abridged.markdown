---
title: Security in the Age of the Internet of Things (abridged)
layout: post
---

<link rel="canonical" href="http://techpoint.org/2017/05/security-age-internet-things/" />

*Originally published at [TechPoint](http://techpoint.org/2017/05/security-age-internet-things/).*

The Internet of Things is [growing fast](https://www.postscapes.com/internet-of-things-market-size/). Connecting so many devices leads to better decisions, safety, and efficiency. But with this comes new security challenges. We, as the defenders, are in a constant arms race against malicious actors. They can fail to attack a system one hundred times and be no worse off. But it only takes one mistake in our defense for them to win. We have seen these growing pains countless times before (and will again) as technology changes.

## What makes IoT security different?

Now that the number of devices involved is so much larger, there is a larger impact if things go wrong. Why is that?
* Many of these devices are being made by companies without a strong background in security
* Speed to market is a key metric in this emerging market
* This encourages companies to do the bare minimum for security
* Security is not a competitive advantage, so it often further deprioritized
* Businesses often focus on the next version, leaving minimal support for released products
* Deploying updates to already-released devices requires an investment in infrastructure

In short, security is rarely made a priority and given enough time or money.

## Won't the market self-correct?

Not with the current economic incentives: the cost of failure is externalized. Bruce Schneier [has a great explanation](https://www.schneier.com/essays/archives/2016/10/we_need_to_save_the_.html):
> Think of all the CCTV cameras and DVRs used in the [attack against Brian Krebs](https://krebsonsecurity.com/2016/09/krebsonsecurity-hit-with-record-ddos/). The owners of those devices do not care. Their devices were cheap to buy, they still work, and they do not even know Brian. The sellers of those devices do not care: they are now selling newer and better models, and the original buyers only cared about price and features. Insecurity is what economists call an externality: it's an effect of the purchasing decision that affects other people. Think of it kind of like invisible pollution.

This is similar to how credit card fraud primarily affects [merchants and banks](https://www.troyhunt.com/relax-its-only-your-credit-card-near/), not the end user. In fact, some criminals find it more lucrative to keep their presence hidden and [rent out the compromised device](https://krebsonsecurity.com/2011/04/is-your-computer-listed-for-rent/).

## Why should consumers care?

A [new type of malware](https://arstechnica.com/security/2017/04/rash-of-in-the-wild-attacks-permanently-destroys-poorly-secured-iot-devices/) is spreading that [permanently disables](https://www.bleepingcomputer.com/news/security/new-malware-intentionally-bricks-iot-devices/) any [vulnerable IoT devices](https://www.theregister.co.uk/2017/04/08/brickerbot_malware_kills_iot_devices/) it can find. If this trend continues, customers will now be directly impacted.

Devices like the [Amazon Echo](https://twitter.com/amazonecho) (powered by Alexa) are becoming more and more popular. Alexa must listen to (but not necessarily record) _everything_ that it can hear. What is the risk profile of an Echo (or similar device) being compromised?

Some IoT devices track health or fitness data (e.g. heart rate, temperature, footstep count, etc.) that can reveal a lot about you. How active you are and when can reveal when you are out of the house on your morning jog and your sleep patterns. Trends in this data can reveal if you are ill or have a chronic medical condition. Samsung's new smart refrigerator can [report its contents](http://newatlas.com/samsung-family-hub-smart-fridge/41192/), which could reveal if you are on vacation. The type of food you eat reveals information about your health. The cost of the food you eat can tell a picture of your finances. On the small scale, this is invaluable for targeting individuals. On a larger scale, this information can be used to build profiles of consumers, which is [nothing new](http://www.nytimes.com/2012/02/19/magazine/shopping-habits.html), but now far more intrusive.

## Why should businesses care?

Liability is murky in many of these cases (having not been tested in the courts), but there is a lot at stake. Take cars, for example. On the _relatively_ tame end of the vulnerability spectrum is being able to get access to [sensitive data on the car and its owner](https://www.troyhunt.com/controlling-vehicle-features-of-nissan/) (which is still a big deal!). On the scarier side is the risk that [hackers could exert more control](https://www.wired.com/2015/07/hackers-remotely-kill-jeep-highway/) over a big packet of kinetic energy with squishy humans inside.

For businesses, IoT devices are likely the weakest link in a security strategy. A compromised IoT device could easily lead to a far more serious breach. Attackers use such breaches to [extort money](https://securityintelligence.com/ddos-extortion-easy-and-lucrative/) from businesses. With a high potential cost of failure, even an [empty threat](http://www.computerworld.com/article/3061813/security/empty-ddos-threats-deliver-100k-to-extortion-group.html) cannot be ignored.

## Where do we go from here?

The media can help by separating fact from fiction. ["Hotel ransomed by hackers as guests locked out of rooms"](https://www.thelocal.at/20170128/hotel-ransomed-by-hackers-as-guests-locked-in-rooms) was a sensational headline that certainly drew some attention. But [it wasn't true](http://www.tomshardware.com/news/ransomware-didnt-lock-hotel-rooms,33528.html) and only added to the [fear, uncertainty, and doubt](https://en.wikipedia.org/wiki/Fear,_uncertainty_and_doubt) surrounding the issue.

The economic incentives described above need to change. We need to align manufacturers and consumers so security is at least considered. I'm not optimistic about this happening on its own. Historically, the free market does not address externalized problems well. You may have heard of the [tragedy of the commons](https://en.wikipedia.org/wiki/Tragedy_of_the_commons). This is where the [government might have to step in](http://www.computerworld.com/article/3136650/security/after-ddos-attack-senator-seeks-industry-led-security-standards-for-iot-devices.html). No one likes regulations, but sometimes they are necessary. It works for pollution and it [could work here](https://www.schneier.com/blog/archives/2016/11/regulation_of_t.html).

We in the industry can help by making it easier to get security right. Stronger [industry-supported guidelines](https://www.schneier.com/blog/archives/2017/02/security_and_pr.html) would go a long way towards setting a baseline expectation. Besides the purely technical concerns, we need guidelines for design and user experience. [Mika Stahlberg](https://safeandsavvy.f-secure.com/2015/08/24/6-reasons-the-internet-of-things-is-difficult-to-secure/) rightfully points out that "ease-of-use, especially during set up, is critical for these kinds of products." Making security features more accessible to the consumer would go a long way towards improving security.

Whether we are businesses, journalists, technologists, or consumers, we need to enter this brave new world with eyes wide open. And while I hope my post freaks you out a little, I'm excited to see how we all come together to figure it out.
