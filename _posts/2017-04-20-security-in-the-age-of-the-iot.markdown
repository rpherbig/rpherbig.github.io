---
title: Security in the Age of the Internet of Things
layout: post
---

<link rel="canonical" href="https://sep.com/blog/security-age-internet-things/" />

The Internet of Things is big. No, really big. No, even bigger than that. How big? My colleague Brad Boyer explains it better than I could (and handily defines the *thing* part of IoT, too). [Go read it](https://www.sep.com/sep-blog/2015/10/22/how-big-is-iot/) - I'll wait.

Welcome back!

Security is hard. No, really hard. Ok, maybe not quite as hard as that. But it is easy to get wrong. Easy enough that [OWASP](https://www.owasp.org/) publishes the [Top 10 Most Critical Security Risks](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) every few years, along with how to mitigate those risks. Yet those same vulnerabilities still appear in the wild. It is why we have sites like [have i been pwned?](https://haveibeenpwned.com/).

> The S in IoT stands for security

> [@lino](https://twitter.com/lino/status/776082366037102592)

## There are new attack vectors

Many of the current-day IoT devices are only recently Internet-enabled. In some cases, they're only recently even *digital*. This is a radical shift in capabilities and platforms which results in new attack vectors that we are still trying to understand. We need to explore the implications of new devices with new capabilities in new contexts.

A perfect example is the prevalence of accelerometers. They are in nearly every smart phone out there, as well as other devices people keep on their person like pedometers. However, many people do not know they are a component in their devices, and many of those devices trust the accelerometer data too much. Who would think of an accelerometer as an attack vector? [These researchers](https://spqr.eecs.umich.edu/papers/trippel-IEEE-oaklawn-walnut-2017.pdf), for one. They came up with a series of [acoustic attacks](https://spqr.eecs.umich.edu/walnut/) that can inject false data.

[Alexa](https://developer.amazon.com/alexa) is the voice service that powers the Amazon Echo. This allows customers to use their voice to interact with devices. It is a great capability to have around the house, but its risk profile has to be carefully considered. We all know someone that enjoys pranks (there is a relevant [XKCD][] for everything!) But I bet most customers never considered what could happen if a newscaster accidentally [used the magic words](http://www.cw6sandiego.com/news-anchor-sets-off-alexa-devices-around-san-diego-ordering-unwanted-dollhouses/) on TV.

I hope the buyer understood the implications of buying a [wireless-enabled sniper rifle](https://www.wired.com/2015/07/hackers-can-disable-sniper-rifleor-change-target/). I hope the city council understood the implications of investing in [light bulbs that could talk to each other](http://iotworm.eyalro.net/).

## New types of data can be exposed in a breach

Speaking of Alexa (see what I did there?), people are now realizing that in order to react to voice commands, Alexa must listen to (but not necessarily record) *everything* that it can hear. Some people are comfortable with that and some are not, but it is something about which all customers need to be aware.

> Once it detects the wake word, according to Amazon, the Echo starts streaming audio to the cloud, where it is secured until the customer permanently deletes it.

Detectives [requested access to the audio data](https://www.nytimes.com/2016/12/28/business/amazon-echo-murder-case-arkansas.html) from an Echo in a murder case. What is the "reasonable expectation of privacy" when [dealing with a device that is always listening](http://nymag.com/selectall/2016/12/can-an-amazon-echo-testify-against-you.html)? What happens if [police misunderstand how the technology works](https://www.washingtonpost.com/news/the-switch/wp/2016/12/28/can-alexa-help-solve-a-murder-police-think-so-but-amazon-wont-give-up-her-data/)?

Let us look at a different data point: your heart rate. That can tell you a lot about someone. How active they are, and when. When they are asleep. If they are ill or have a chronic medical condition. Pacemakers are an obvious collector of that data. Indeed, in [at least one case](https://www.washingtonpost.com/news/to-your-health/wp/2017/02/08/a-man-detailed-his-escape-from-a-burning-house-his-pacemaker-told-police-a-different-story/) that data was used to [prove arson and insurance fraud](http://www.networkworld.com/article/3162740/security/cops-use-pacemaker-data-as-evidence-to-charge-homeowner-with-arson-insurance-fraud.html). Now there are more and more devices that a user might not expect to record their heart rate (for example, pedometers). One couple [found out they were pregnant](http://mashable.com/2016/02/10/fitbit-pregnant/#f5IK5c8vDPqT) via their FitBit data.

Imagine what would happen if the data store were breached. Building profiles of consumers is [nothing new](http://www.nytimes.com/2012/02/19/magazine/shopping-habits.html), but now there are more ways to gather more data.

Samsung's new smart fridge can [report its contents](http://newatlas.com/samsung-family-hub-smart-fridge/41192/). What is the risk profile of that data being leaked? If your fridge is empty, maybe you're on vacation. The type of food you eat affects your health. The cost of the food you eat gives a glimpse into your finances. This information could be valuable to a malicious actor. A smart thermostat could have [similar risks](https://www.youtube.com/watch?v=DKE-pWA68Ac).

Children's toys are now joining the IoT, which brings up new privacy concerns. Germany has already [banned one such toy](http://www.telegraph.co.uk/news/2017/02/17/germany-bans-internet-connected-dolls-fears-hackers-could-target/), and security researchers are [concerned about another](http://www.huffingtonpost.com.au/entry/hello-barbie-security-concerns_us_565c4921e4b072e9d1c24d22). When sensitive data is held by a third party, consumers need to consider the worst case. What happens when [kids' voice messages are leaked](https://motherboard.vice.com/en_us/article/internet-of-things-teddy-bear-leaked-2-million-parent-and-kids-message-recordings)? Won't somebody please [think of the children](https://www.youtube.com/watch?v=RybNI0KB1bg)?

## Vulnerabilities are common and easy to find

IoT devices are marketed at a very broad audience, meaning consumers are less likely to be technologically adept. That makes [secure default settings](https://krebsonsecurity.com/2016/02/iot-reality-smart-devices-dumb-defaults/) critically important, which many devices do not have. Even worse, many do not make it easy to change those defaults even if the consumer is aware of the need.

Manufacturers commonly load devices with a default username and password, which is [easily looked up](http://www.routerpasswords.com/). However, some devices take this a step further and have hardcoded credentials which the [user *cannot* change](http://blog.talosintelligence.com/2016/02/trane-iot.html). Typically these hardcoded credentials are [not even mentioned to the user](https://www.flashpoint-intel.com/blog/cybercrime/when-vulnerabilities-travel-downstream/), leaving them unaware of a large hole in their security profile. One of the more recent and nefarious malware packages, Mirai, scans for IoT devices that have [known credentials](https://ipvm.com/reports/ip-cameras-default-passwords-directory).

In many cases a single manufacturer produces many devices with different brands (this is known as a [white label product](https://en.wikipedia.org/wiki/White-label_product)). The wide-spread nature of this business practice leads to what is known as a [class break](https://www.edge.org/annual-question/2017/response/27229), where one smart person can come up with one clever hack that [breaks an entire class of systems](https://blog.sucuri.net/2016/09/iot-home-router-botnet-leveraged-in-large-ddos-attack.html). In fact, that is exactly what happened when the Mirai author [released their source code](https://krebsonsecurity.com/2016/10/source-code-for-iot-botnet-mirai-released/). That malware [is not even very advanced](https://motherboard.vice.com/en_us/article/internet-of-things-malware-mirai-ddos), but it nonetheless effective. If a vulnerability is found in one device, many other brands and models may [also be affected](https://pcidss.wordpress.com/2016/10/10/iot-botnets-white-label-risks-bad-customer-experience-and-what-it-means-from-our-post-iot-attack-analysis-threatpost/). Discovering which devices are the same, however, is something the vendors [do not make easy](https://krebsonsecurity.com/2016/10/who-makes-the-iot-things-under-attack/).

Vulnerable devices have never been easier to find. There is even a [search engine for the Internet of Things](https://www.shodan.io/). Shodan makes it easy to [search the web for IoT devices](https://arstechnica.com/security/2016/01/how-to-search-the-internet-of-things-for-photos-of-sleeping-babies/).

## Vulnerabilities are hard to fix

Windows users have only recently gotten used to regularly updating their computers, and Microsoft has been working on that for many years. How many people think "it's Tuesday, time to check if my refrigerator needs any software updates"? Many IoT devices are [not even designed to be updated](https://www.wired.com/2014/01/theres-no-good-way-to-patch-the-internet-of-things-and-thats-a-huge-problem/). This means once a vulnerability is discovered, it is only a matter of time until that device is compromised. Even if the device is factory reset, without an update it will be breached again. Even for some of the devices that support updates, [it is not always easy](https://www.trane.com/residential/en/resources/smart-home-automation/installing-upgrading.html). Combine that with the fact that some of the devices have an expected lifespan of 10 or more years and you can see how big of a problem this is.

## Why should businesses and consumers care?

I have described above what could happen in the event of a breach. Some sensitive data could be leaked with some serious consequences. But there are more reasons than that.

One easy answer is that a vulnerable IoT device is likely the weakest link in a security strategy. A compromised IoT device has nearly the same threat profile as any other compromised device on a network.

What if "we do not have anything of value on our [network/site/etc.]"? You still have your [reputation to think of](https://www.troyhunt.com/all-websites-have-something-of-value-for-attackers-reputation/).

Malicious actors are now using some compromised devices to anonymize their activity. The device is [turned into a proxy](https://krebsonsecurity.com/2016/10/iot-devices-as-proxies-for-cybercrime/) through which the hacking, spamming, DDoS, or other attacks are launched. This makes it harder to catch the criminals, and introduces the possibility of innocent people being caught up in the investigation.

Unfortunately, with the [proliferation of vulnerable devices](https://krebsonsecurity.com/2016/12/researchers-find-fresh-fodder-for-iot-attack-cannons/) and malware that can compromise them, criminals are building massive botnets. They use these botnets to [extort money](https://securityintelligence.com/ddos-extortion-easy-and-lucrative/), [censor opponents](https://krebsonsecurity.com/2016/09/the-democratization-of-censorship/), or whatever [they can make money doing](https://www.forbes.com/sites/thomasbrewster/2016/10/23/massive-ddos-iot-botnet-for-hire-twitter-dyn-amazon/). Even an [empty threat](http://www.computerworld.com/article/3061813/security/empty-ddos-threats-deliver-100k-to-extortion-group.html) is enough, sometimes. And these attacks are only [growing in scale](http://hub.dyn.com/static/hub.dyn.com/dyn-blog/dyn-statement-on-10-21-2016-ddos-attack.html) as [time goes on](http://www.ibtimes.co.uk/biggest-ever-terabit-scale-ddos-attack-yet-could-be-horizon-experts-warn-1588364).

Liability is murky in many of these cases, until it is tested in the courts, and there is a lot at stake. Take cars, for example. On the tame end of the vulnerability spectrum is being able to get access to [sensitive data on the car and its owner](https://www.troyhunt.com/controlling-vehicle-features-of-nissan/) (still a big deal!). On the scarier side is the risk that [hackers could exert more control](https://www.wired.com/2015/07/hackers-remotely-kill-jeep-highway/) over a big packet of kinetic energy with squishy humans inside.

## So why don't they care?

Thankfully, Bruce Schneier [has a great explanation](https://www.schneier.com/essays/archives/2016/10/we_need_to_save_the_.html):
> Think of all the CCTV cameras and DVRs used in the [attack against Brian Krebs](https://krebsonsecurity.com/2016/09/krebsonsecurity-hit-with-record-ddos/). The owners of those devices do not care. Their devices were cheap to buy, they still work, and they do not even know Brian. The sellers of those devices do not care: they are now selling newer and better models, and the original buyers only cared about price and features. Insecurity is what economists call an externality: it's an effect of the purchasing decision that affects other people. Think of it kind of like invisible pollution.

This is similar to how credit card fraud primarily affects [merchants and banks](https://www.troyhunt.com/relax-its-only-your-credit-card-near/), not the end user.

Criminals sometimes find it more lucrative to keep their presence hidden and [rent out the compromised device](https://krebsonsecurity.com/2011/04/is-your-computer-listed-for-rent/).

Maybe consumers will start to take notice if a [new trend of malware](https://arstechnica.com/security/2017/04/rash-of-in-the-wild-attacks-permanently-destroys-poorly-secured-iot-devices/) continues to spread that [permanently disables](https://www.bleepingcomputer.com/news/security/new-malware-intentionally-bricks-iot-devices/) any [vulnerable IoT devices](https://www.theregister.co.uk/2017/04/08/brickerbot_malware_kills_iot_devices/) it can find.

## Why is IoT different than what we have seen in the past?

These are the growing pains we have seen countless times before (and will again in the future) across various industries. Devices are being connected in new and novel ways. The "arms race" between attack and defense is changing very rapidly. New techniques are being developed on both sides.

However, now the number of devices involved is much larger, with a correspondingly larger impact if things go wrong. Why is that?
* Never before have so many connected devices been so physically accessible
* Many of these devices are being made by companies without a strong background in security
* Speed to market is a key metric in this emerging market
* This lends itself to cutting corners (or doing the bare minimum) when possible
* Security is not a competitive advantage, so it often deprioritized
* Supporting products after manufacturing requires a certain mindset (businessset?)
* Deploying updates (or at least notifying the public of vulnerabilities) requires an investment in infrastructure

In short, security is not often made a priority or given enough attention (either time or money).

Won't the market self-correct? Not with the current economic incentives. Neither the manufacturer nor consumer have a reason to prioritize security because the cost of failure is externalized. Even if the consumer were security conscious, there is too much [information asymmetry](https://en.wikipedia.org/wiki/Information_asymmetry) between consumers and manufacturers. Consumers cannot easily find most of the information they would need to truly evaluate competing products.

## Where do we go from here?

Probably the most important things is to carefully separate truth from fearmongering. ["Hotel ransomed by hackers as guests locked out of rooms"](https://www.thelocal.at/20170128/hotel-ransomed-by-hackers-as-guests-locked-in-rooms) makes for a sensational headline - it is sure to get a bunch of clicks. But [it wasn't true](http://www.tomshardware.com/news/ransomware-didnt-lock-hotel-rooms,33528.html) and only added to the [fear, uncertainty, and doubt](https://en.wikipedia.org/wiki/Fear,_uncertainty_and_doubt) surrounding the issue. This is how we make sure we are solving the right problems, and not protecting against unrealistic [movie plot threats](https://www.schneier.com/blog/archives/2006/04/announcing_movi.html).

We need to change the economic incentives described above. To align manufacturers and consumers so security is at least considered. It is even better if consumers can be aware of the risks that the IoT introduces and deliberate about their use of these devices. However, I am not optimistic about this. Historically, the market does not address externalized problems well.

That is where [government regulation comes in](http://www.computerworld.com/article/3136650/security/after-ddos-attack-senator-seeks-industry-led-security-standards-for-iot-devices.html). No one likes regulation for its own sake. No one wants the government involved unless it is necessary. But regulation works for pollution and other externalized problems (you've probably heard of the [tragedy of the commons](https://en.wikipedia.org/wiki/Tragedy_of_the_commons)), and it [could work here](https://www.schneier.com/blog/archives/2016/11/regulation_of_t.html) too.

At the same time, we need to find a way to make security easier to get right. For software and hardware development, [industry-supported guidelines](https://www.schneier.com/blog/archives/2017/02/security_and_pr.html) would go a long way to setting a baseline expectation. In addition to the purely technical concerns, we need guidelines for design and user experience. [Mika Stahlberg](https://safeandsavvy.f-secure.com/2015/08/24/6-reasons-the-internet-of-things-is-difficult-to-secure/) rightfully points out that "ease-of-use, especially during set up, is critical for these kinds of products". Making security features more accessible to the consumer would go a long way towards improving security.

[XKCD]: https://xkcd.com/1807/ "Listening"
