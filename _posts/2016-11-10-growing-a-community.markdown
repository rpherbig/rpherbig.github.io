---
title: Growing a Community
layout: post
---

This is part of an ongoing series of posts about a side project I am working on with [Rob Uhl](http://rcuhljr.github.io/):

* [Introduction - A Lot Can Happen in a Year](/2016/09/30/a-lot-can-happen-in-a-year.html)
* [Building Your Castle in a Swamp](http://rcuhljr.github.io/blog/2016/10/07/side-project-lessons-part1.html)
* [Dependency Resolution](http://rcuhljr.github.io/blog/2016/10/19/side-project-lessons-part2.html)
* [Why Are We Writing These Scripts?](/2016/10/31/why-are-we-writing-these-scripts.html)

-----

## The DragonRealms community

> com·mu·ni·ty

> 1. **a group of people living in the same place or having a particular characteristic in common.**
> 2. a feeling of fellowship with others, as a result of sharing common attitudes, interests, and goals.
> 3. a group of interdependent organisms of different species growing or living together in a specified habitat.

When I started playing DragonRealms (DR), I wasn't really focused on the community. I was busy learning new mechanics, exploring the world, and listening to Rob wax nostalgic about his time in DR (15 years ago). And to be honest, the game systems themselves somewhat discouraged new players from interacting with other players:

* I had no money to buy things from the community, and no skills that can contribute back to the community (e.g. crafting)
* Most of my time was spent hunting rats to make enough coin to repair my gear to get back out hunting rats
* Specific player-made items (which I could not afford) are needed to access most of the in-game chat systems
* Many questions were answered with a link to the [(mostly) official wiki](https://elanthipedia.play.net/Main_Page), but just enough content is inaccurate or out of date to confuse a new player
* There is a newbie help chat system which includes other newbies and volunteer mentors (members of the DR community who are of above-average helpfulness) - though as volunteers, they aren't always available
* The character-growth model of DR (perhaps the subject of a future blog post) encourages players to maximize the number of skills they train, which disincentivizes players from spending time idle (e.g. chatting or helping a new person)

I mean, you *know* you are part of a community when you play a multiplayer game, but at first you don't really KNOW it... you know? Luckily for me, Rob was a great help, as were a few other players I ran into by seeking out popular hangout spots. And as with any other community, there is a learning curve: 20 years of informal rules, systems, and conventions have formed. Some of those are unspoken, undocumented, and few people will take the time to explain them. Ask me about the NPC healer sometime... It's also hard when most of the in-game chat systems are strictly "in character" - that is, from your character's point of view. It's hard to get Ogg the Barbarian to explain the nuances of a complex system, even if Ogg's player wants to help.

DR's chat channels have the [usual problems](https://www.penny-arcade.com/comic/2004/03/19) (strong language warning!) that crop up when you mix a normal person, anonymity, and an audience. There are some official policies around how this is kept in check, and the topic comes up constantly in DR forum discussions. There are even changes being implemented right now to the chat systems to try and reduce trolling and griefing (being deliberately irritating to upset others). I suspect there are many reasons for this, and it's not an easy problem to solve.

## The Lich community

> com·mu·ni·ty

> 1. a group of people living in the same place or having a particular characteristic in common.
> 2. **a feeling of fellowship with others, as a result of sharing common attitudes, interests, and goals.**
> 3. a group of interdependent organisms of different species growing or living together in a specified habitat.

One of the things that [Lich](https://lichproject.org/) supports by default is a set of chat channels (hereafter, Lnet) that go through the Lich servers, rather than the DR servers. That means those channels do not need to adhere to the DR policies. DR does not ([and will not](http://forums.play.net/forums/DragonRealms/The%20Moon%20Mages/General%20Discussions%20-%20Moon%20Mages/thread/1811680)) support out-of-character (OOC) chat, whereas Lnet does.

I believe this strengthens the Lich community - I've seen wonderful conversations on Lnet about life, careers, and relationships. In addition, the Lich community is much more positive than that of DR in general. I constantly see people healing others, discounting services (or even giving services and items away), answering questions on game mechanics or scripts, and so on. This cooperation and collaboration has a positive feedback effect.

There are a few training strategies that have become pretty popular in the Lich community (optimizing training would be a good future blog post), one of which requires a specific item that is hard to get. One generous Licher went and bought 20 of the item and handed them out to everyone that needed one - but they still had 10 left over. They wanted a way to make the items accessible to other Lichers in the future, but DR does not have an easy way to do that. In order to support cooperation, we created a character who only exists to share items within the community. Anyone can contribute items or request them.

We have another player whose character is a healer. He could be out in the game world training, but instead has decided to contribute back to the community by making himself available to heal Lichers. Everyone knows to first check if he is around before finding another healer (who are often slower and charge money for their services).

The Lich community is also resilient to disruption. A few months ago some well-known trolls and griefers joined Lnet. With their usual tactics, they tried to antagonize Lichers, who wisely decided not to engage with their antics. Instead, we simply continued having fun. Without people feeding their bad behavior, they got bored and either left or stopped being disruptive. Either way, the Lich community is better for it (and maybe we converted some of them to be productive members!). I hope that as we get more popular and our population grows, we will continue to foster good behavior.

## A community within a community

> com·mu·ni·ty

> 1. a group of people living in the same place or having a particular characteristic in common.
> 2. a feeling of fellowship with others, as a result of sharing common attitudes, interests, and goals.
> 3. **a group of interdependent organisms of different species growing or living together in a specified habitat.**

When we [began writing our scripts](https://github.com/rpherbig/dr-scripts/commit/1f41330ff94a3220ae80d89f29b91304c1382f80), we took a very Agile approach. Write what we needed for our characters, add settings and configuration that worked for us, and expand the scripts' capabilities over time as we encountered new needs or edge cases. This was fantastic for rapid development - getting the most functionality in the least development time.

But it also meant that we tackled error paths and edge cases as we encountered them. Our code was not perfectly robust from the start, and for the most part, that was fine. Most errors just stopped a script, and since we were at the keyboard, we would fix the problem and restart it. At worst a character might lose an item (ask Rob about his cleric's shield sometime).

But occasionally, rarely, there would be a bug that was *noisy*. Typically these errors would be a broken `while` loop or bad conditional `return` that would result in spamming a room with commands. Even if we reacted in a few seconds, hundreds of commands would have been sent. After the first of these it was clear that we had to be responsible members of the scripting (and/or Lich) community, as members of the larger DR community.

To that end, we implemented a few different strategies in our scripts:

* Be deliberate about pausing between commands or actions. In many cases, this is as simple as sending an action, then waiting until we see text that indicates the action was taken.
* Check for repeated actions. For example, movement: do not go to one room only to immediately leave for a second room; instead we write a bit more code to detect this case and go directly to the second room.
* Use timers to check for infrequent game state changes, rather than checking more frequently. For example, characters can teach a class, but this is rare. We only check for active classes every few minutes.
* Avoid using common hangout spots for training. This keeps spammy training processes away from players that want to congregate and interact with each other.

The truth is that we need to be careful that our scripts do not negatively impact those around us. Furthermore, we need to be acutely aware of the *perception* of others in the DR community. Even though we are following the [official scripting policy](https://elanthipedia.play.net/Policy:Scripting_policy), some people take offense to our use of scripts. It is common for those players to try to break our scripts, for example, by slipping an item into a character's hand. Our scripts need to be robust and handle unexpected game state, as well as being careful when recovering from an error.

## Testimonials

I asked on Lnet what they thought about the Lich community (names have been removed for privacy):

Person 'K1':

> The collaborative effort is certainly helpful. Lnet is extremely helpful. Whereas my experiences with genie [an alternative front end and scripting solution] were rather... solo. Even when my friend and i helped develop some plugins for genie, it still felt like the community kept the best secrets to individuals. Knowledge-sharing wasn't a big thing. it was still the "i'll share a bit, but my script will always be better". For example, the necro healing conversation that we've have been having. Wouldn't have really happened when i was rockin' genie seriously.

Person 'M':

> The community aspect definitely isn't something to understate.  DR-lich is super friendly and helpful.

Person 'A':

> By the way just wanted to thank everyone in lich for being so helpful. I wasn't sure if I was going to stick around but going to be upgrading my account and unlocking my old one.

Person 'F':

> I just started playing this again because they sent out free codes. If it weren't for the lich community, I'd be gone again already.

Person 'K2':

> I think the real linchpin of Lich is the fact that so many of us remain _because of_ Lnet. Lnet demonstrates that OOC chat can be friendly and helpful. I've read on the official forums that Lnet chat is horrible and trollish, and that just has not been my experience. We've managed to not have Lnet turn into Barrens chat, as it were. I suspect because collectively we've gone out of our way to be helpful, whereas the game world simply doesn't allow for it in meaningful ways.
