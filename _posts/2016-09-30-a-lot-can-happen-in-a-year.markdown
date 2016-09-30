---
title: A Lot Can Happen in a Year
layout: post
---

One year ago (346 days, but who's counting?), [Rob Uhl](http://rcuhljr.github.io/) introduced me to [DragonRealms](http://www.play.net/dr/) (DR), a game he played many years ago. [DragonRealms](https://en.wikipedia.org/wiki/DragonRealms) is an online text-based role playing game (RPG), also known as a [multi-user dungeon](https://en.wikipedia.org/wiki/MUD) (MUD). MUDs were the precusors to today's massively multiplayer-online games (MMOs). I played many a MUD back in the day, though not this one, so I was interested. DR used to require a paid subscription to play, but the recently added free to play (F2P) option made the barrier to start playing virtually nonexistent.

In true RPG fashion, DragonRealms has a very large set of skills that impact your gameplay. But unlike many RPGs, you gain experience and levels for each skill independently, and the experience gain is based on your usage of that skill. Want to get better at swinging a sword? Go swing a sword a lot. But that won't help you swing a mace or craft some armor.

It quickly became apparent that some parts of the game were very repetitive. For example, you first have to climb hundreds of trees to train up your Athletics skill before being able to take a shortcut (swimming across a river instead of waiting on a ferry). This is analogous to the 'treadmill' effect in many MMOs. Don't get me wrong - there are many interesting and non-repetitive parts of the game, but in some cases you have to slog through the tedium to get to the good parts.

Why should you care? Why am I telling you this? Well, like any good software engineers, we saw an opportunity to automate the boring parts. So we set out on a year-long journey (that is still ongoing).

The default front end had some [basic scripting capabilities](https://www.play.net/playdotnet/play/stormfront_scripting.asp): regex matching, loops, and labels/GOTOs - very BASIC-like. You can imagine how much fun that was to use. Even a basic script like [selling gems](https://elanthipedia.play.net/Gem_Seller_(script)) could run over 700 lines. And there's not really a meaningful way to debug that mess if you make a mistake. It's the Volkswagen of scripting languages - it'll get you where you want to go, but it'll be uncomfortable. That lasted about a week before we started looking for other options. We evaluated several and ended up picking one, [Lich](https://lichproject.org/), and a year later we've written 20,000 lines of Ruby.

"But Herbig, you yada yada'd over the best part!" I hear you say. That's right - no one writes 20,000 lines of code without some good stories to tell. Rob and I will be writing more posts in the future about some of the interesting things we've done for this project.

In the meantime, I'll leave you with some numbers, because who doesn't love numbers?

* [First commit](https://github.com/rpherbig/dr-scripts/commit/1f41330ff94a3220ae80d89f29b91304c1382f80): Oct 16, 2015
* 17 contributors
* 3468 commits
* 705 issues
* 166 closed PRs
* 20,240 lines of Ruby (code)
* 7,941 lines of YAML (configuration and data)

Spoiler alert: it's pretty awesome.

GL HF
