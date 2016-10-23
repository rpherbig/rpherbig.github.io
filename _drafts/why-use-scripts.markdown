---
title: Why Use Scripts?
layout: post
---

This is part of an ongoing series of posts about a side project I am working on with [Rob Uhl](http://rcuhljr.github.io/):

* [Introduction - A Lot Can Happen in a Year](/2016/09/30/a-lot-can-happen-in-a-year.html)
* [Building Your Castle in a Swamp](http://rcuhljr.github.io/blog/2016/10/07/side-project-lessons-part1.html)
* [Dependency Resolution](http://rcuhljr.github.io/blog/2016/10/19/side-project-lessons-part2.html)

-----

We've talked a lot about the infrastructure we're working with, but haven't spent much time on what it is we're actually building (or, for that matter, why). At a high level, a script is simply a Ruby file with the `.lic` extension. In a less literal sense, a script is a way to automate some manual steps. It can only do what a user can do, albeit with more speed and accuracy.

## Why use scripts?

Speed and accuracy are definitely advantages over not using scripts - not to mention making sure you don't forget a step when doing something involved. Many games have taken the approach of disallowing scripting in any real sense (see: World of Warcraft macros). [DragonRealms](https://www.play.net/dr/) (DR), however, has quite a liberal [scripting policy](https://elanthipedia.play.net/Policy:Scripting_policy).

DR has been in development for over 20 years. Over that time, many systems have been introduced, modified, removed, and reimplemented. As in any large-scale software effort, sometimes the new and old system coexist for a time. Sometimes a very long time. For example, there are hundreds of non-player characters (NPCs) from whom you buy various items. Some of these NPCs use an one system in which you must `read` from an item in the room to see what they sell (a catalog, a register, or several other nouns). Then you issue the `buy` command, which does not actually buy the item, but instead asks them how much they want for it. Then you `offer` the amount to complete the transaction. Other NPCs use a system in which you `order` to see what they have available, then `order item` to complete the transaction. A subset of those instead treat `order item` as a request, which then requires you to `order item` again to complete the transaction.

I consider remembering which NPC uses which system to be cruft. Mental overhead. For me, dealing with three different ways just to buy an item from an NPC takes me out of the game - it breaks my mental model. I want to think at the 'buy an item' level of abstraction. So I wrote some code in a script once that deals with the *how*, letting me think in terms of *what*.

## Focus on what is fun

Let's look at crafting (I'll be using Forging for these examples, but the points apply to all crafts). In DR, it is very involved - there are many steps, each in the right order, and you have to watch for random mistakes to appear and then correct them. One persons deep, rewarding, and immersive crafting experience is another persons tedium. That's where scripts come in: letting you, the player, think at whatever level of abstraction is the most fun for you. I think that's pretty awesome.

At the lowest level of abstraction is the player that wants to do it by hand (and there's nothing wrong with that!). They're going to type `pound ingot on anvil with my hammer`, wait to see if their character made a mistake (such as because they're making a difficult item relative to their skill level), then `push my bellows` to keep the flames hot, and continue until done. Very immersive, very much a role-playing game. You can practically feel the heat on your face as you read the text (seriously - the text is DR is very well-written):
> Sparks fly into the air as you transfer the scissors back and forth between the forge fires and the anvil, alternating heating with vigorous hammering of the metal.  The work proceeds as planned and you avoid introducing any defects.

But for those that want it, we have a script called `forge` which automates the crafting steps only. It starts with an ingot and ends with a finished item. You are responsible for procuring an ingot, finding an unused anvil, and so on. But if you don't find that part fun, we also have a script called `smith` that will take care of buy an ingot from an NPC, search out an unused anvil, and then start crafting.

The beauty of this system is that scripts are purely additive - they do not take away from the game. They are tools in your toolbox, only doing as much or as little as you want them to. And your need can easily change over time. The first time you craft, you should do it by hand to understand how the process works. The 300th time you make something, you may decide to use a script. And because of the experience and skill model of DR, if you want to practice a craft, you'll eventually make that 300th item (or 3000th...).

## But don't take my word for it

I asked some of the folks using our scripts what they thought:

> I use scripts to train, and perform matters of rote for me so that I can spend the time I would normally be available to play as an opportunity to roleplay and interact with others instead of feeling pressured to work on progressing. Without scripting i feel like i have to choose between roleplaying and making progress given the time sink involved. Scripting enables me to enjoy both sides with giving one up.


> I find watching my character play the game through logic I've written (or some else) is really satisfying. Writing a script to do some complicated task, watching it fail terribly, fixing it and then finally when it works for the first time; it feels like an accomplishment. And less to the point, you have this really nice collaborative project going so we can all share and improve on each others work. Also time is a precious commodity for people, having it spent on braiding grass or really any DR skill training is not adding to my immersion in any game world. I think its interesting the first time, so you see a flavor of how it works, read the text, and form a mental image of what your character is doing... but beyond that its just a waste of time really.


> I agree, I think of DR as the ultimate grind [and scripts help with that].


> Just wanted to say thanks again for the amazing amount of work you all do on this. It's changed DR for me.



Truix DR [4:12 PM]
Yeah, scripting in DR isn’t unsurprising. Any game that employs the ‘skill-based’ learning model (i.e. The person who chops 1k trees will be better at lumberjacking than the person who chops 1), usually ends up with this age-old conundrum. The proper ‘solution’ usually relies heavily on the original game design’s progression system.
The “why we script” question isn’t even a decent enough question. The ‘why’ is obvious… or perhaps it was less obvious back in 1999, when scripting engines were less sophisticated, open-source was less of a thing, and custom front ends weren’t being created to work with your game (DR). Improvements in technology has this odd way of making things more efficient (go figure) — when more modern technology (think: better scripts, a ruby script backend like Lich, more sophisticated scripting layers on Genie and SF) finds the C code from your 1996 game, the results is a more malleable and, by proxy, easy game to play.
The age where we leverage technology to make our lives easier isn’t dead and gone — it’s a fact of life an will continue to be. Game that came out in 2016 fall into the same _trap_ of a large subset of the population attempting to ‘crack’ it. Like Crannach pointed out, it’s also part of the game. It may not be the original intent of the game designer for it to be that way, but the moment the public consumes it, I don’t think it’s the game designer’s game (SIMU) any longer (debatable though).







Endraig DR [3:51 PM]
I'd be fine with dragonrealms removing the skill "growth" component and had people simply choose skills, crafts with a finite amount of selections. it's probably the only way they'll ever see any semblance of the old dragonrealms socializing back.
as dumb as that sounds the chase for "end game" is consuming the game and there is no reasonable footing for me to truly roleplay in a place where someone else can always quite literally dominate me because they have an extra year in game.
over something big or small, it can always escalate to pvp and if it does well insta-lose.




http://forums.play.net/forums/DragonRealms/Discussions%20with%20DragonRealms%20Staff%20and%20Players/Complaints/thread/1794299?get_newest=true
  http://forums.play.net/forums/DragonRealms/DragonRealms%20Policy%20Discussions/Scripting%20policy/view/1136
  http://forums.play.net/forums/DragonRealms/Abilities,%20Skills%20and%20Magic/The%20Experience%20System/view/5364


http://forums.play.net/forums/DragonRealms/DragonRealms%20Policy%20Discussions/Scripting%20policy/view/1350
  Find the post by DR-RAESH





From first post:
  It quickly became apparent that some parts of the game were very repetitive. For example, you first have to climb hundreds of trees to train up your Athletics skill before being able to take a shortcut (swimming across a river instead of waiting on a ferry). This is analogous to the ‘treadmill’ effect in many MMOs. Don’t get me wrong - there are many interesting and non-repetitive parts of the game, but in some cases you have to slog through the tedium to get to the good parts.


"Give item to Catrox" vs "give item"

Use of "my" to avoid ground, in buckets, etc.

Target repeated actions, not one-offs
