---
title: Why Are We Writing These Scripts?
layout: post
---

This is part of an ongoing series of posts about a side project I am working on with [Rob Uhl](http://rcuhljr.github.io/):

* [Introduction - A Lot Can Happen in a Year](/2016/09/30/a-lot-can-happen-in-a-year.html)
* [Building Your Castle in a Swamp](http://rcuhljr.github.io/blog/2016/10/07/side-project-lessons-part1.html)
* [Dependency Resolution](http://rcuhljr.github.io/blog/2016/10/19/side-project-lessons-part2.html)

-----

We've talked a lot about the infrastructure we're working with, but haven't spent much time on what it is we're actually building (or, for that matter, why). At a low level, a script is simply a Ruby file with the `.lic` extension. At a higher level, a script is a way to automate some manual steps. It can only do what a user can do, albeit with more speed and accuracy.

## Why use scripts?

Speed and accuracy are definitely advantages over not using scripts - not to mention making sure you don't forget a step when doing something involved. Many games have taken the approach of disallowing scripting in any real sense (see: World of Warcraft macros). [DragonRealms](https://www.play.net/dr/) (DR), however, has quite a liberal [scripting policy](https://elanthipedia.play.net/Policy:Scripting_policy).

DR has been in development for over 20 years. Over that time, many systems have been introduced, modified, removed, and reimplemented. As in any large-scale software effort, sometimes the new and old system coexist for a time. Sometimes a very long time. For example, there are hundreds of non-player characters (NPCs) from whom you buy various items.

* Some of these NPCs use one system in which you must `read` from an item in the room to see what they sell (usually a catalog, a register, or one of several other nouns). Then you issue the `buy` command, which does not actually buy the item, but instead asks the NPC how much they want for it. Then you `offer` the amount to complete the transaction.
* Other NPCs use a system in which you `order` to see what they have available, then `order item` to complete the transaction.
* Some of the NPCs that use `order` treat `order item` as a request, which then requires you to `order item` a second time to complete the transaction.

I consider remembering which NPC uses which system to be mental overhead. For me, dealing with three different ways just to buy an item from an NPC takes me out of the game - it breaks my immersion. I want to think at the 'buy an item' level of abstraction. So I took the time to write a script that deals with the *how*. From now on, I can use that script (and reuse that code in other scripts), letting me think in terms of *what*.

## Focus on what is fun

Let's look at crafting (I'll be using Forging for these examples, but the points apply to all crafts). In DR, it is very involved - there are many steps, each in the right order, and you have to watch for random mistakes to appear and then correct them. One person's deep, rewarding, and immersive crafting experience is another person's tedium. That's where scripts come in: letting you, the player, think at whatever level of abstraction is the most fun for you. I think that's pretty awesome.

At the lowest level of abstraction is the player that wants to do it by hand (and there's nothing wrong with that!). They're going to type `pound ingot on anvil with my hammer`, wait to see if their character made a mistake (such as because they're making a difficult item relative to their skill level), then type `push my bellows` to keep the flames hot, and so on - continuing until the process is complete. Very immersive, very much a role-playing game. You can practically feel the heat on your face as you read the text (seriously - the text is DR is very well-written!):
> Sparks fly into the air as you transfer the scissors back and forth between the forge fires and the anvil, alternating heating with vigorous hammering of the metal.  The work proceeds as planned and you avoid introducing any defects.

But for those that want it, we have a script named `forge` which automates the crafting steps only. It starts with an ingot and ends with a finished item. You are responsible for procuring an ingot, finding an unused anvil, and so on. But if you don't find that fun, we have another script named `smith` that will take care of buying an ingot from an NPC (taking care to use the right verb for each NPC!), search out an unused anvil, and then start crafting.

The beauty of this system is that scripts are purely additive - they do not take away from the game. They are tools in your toolbox, only doing as much or as little as you want them to. And your need can easily change over time. The first time you craft, you should do it by hand to understand how the process works. The 300th time you make something, you may decide to use a script. And because of the experience and skill model of DR (the topic of a future post), if you want to get good at a craft, you'll eventually be making that 300th item (or 3000th...).

## [But you don't have to take my word for it](https://www.youtube.com/watch?v=vAvQbEeTafk)

I asked some of the folks using our scripts what they thought (names have been removed for privacy):

Person 'E':

> I use scripts to train, and perform matters of rote for me so that I can spend the time I would normally be available to play as an opportunity to roleplay and interact with others instead of feeling pressured to work on progressing. Without scripting i feel like i have to choose between roleplaying and making progress given the time sink involved. Scripting enables me to enjoy both sides with giving one up.

Person 'C':

> I find watching my character play the game through logic I've written (or some else) is really satisfying. Writing a script to do some complicated task, watching it fail terribly, fixing it and then finally when it works for the first time; it feels like an accomplishment. And less to the point, you have this really nice collaborative project going so we can all share and improve on each others work. Also time is a precious commodity for people, having it spent on braiding grass or really any DR skill training is not adding to my immersion in any game world. I think its interesting the first time, so you see a flavor of how it works, read the text, and form a mental image of what your character is doing... but beyond that its just a waste of time really.

Person 'I':

> I agree, I think of DR as the ultimate grind and scripts help with that.

Person 'N':

> Just wanted to say thanks again for the amazing amount of work you all do on this. It's changed DR for me.

Person 'V':

> I would also venture to say that in writing a script you’re taking a deeper look at what you’re doing, which is fun. In writing a script you’re taking the time to think about it and make it efficient. You’re thinking about why you’re responding to things and how you react and why. That’s pretty neat. I wish there was a way to force me into that mental framework in everyday life, I’d probably be a better person lol.
