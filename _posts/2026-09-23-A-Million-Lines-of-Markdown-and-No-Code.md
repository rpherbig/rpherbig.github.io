---
title: "A Million Lines of Markdown and No Code"
layout: post
---

<link rel="canonical" href="https://sep.com/blog/a-million-lines-of-markdown-and-no-code/" />

I recently learned about a company that has rebuilt waterfall from scratch – on purpose, with AI – while believing they're doing the most modern software development possible. The oldest failure in software process, the one we spent fifty years learning our way out of, wearing this year's tooling. And the AI is executing it faithfully.

Here's the shape of it. In April, they started rebuilding their flagship product – payroll, purchasing, and invoicing for small businesses. Real money, real beta date: November 1st. The plan: write all the specs first, then AI agents turn them into an application. Five months in, the team has produced a million lines... of markdown. There is no code.

I heard about all this secondhand, laughed, and moved on. But the stories kept coming, each one stranger than the last, so eventually I got in touch with a team member inside the project and asked him to walk me through it from the beginning. Everything specific in what follows comes from him; where I'm inferring instead of reporting, I'll say so. Somewhere in those million lines is a spec directing the payroll system to pull payroll data from the browser's cache. That is a real sentence a real spec says about real payroll data. Nothing upstream ever flagged it. We'll get there.

And fair warning: before I take any of this apart, I'm going to make their case properly, because the thinking that got them here is better than it sounds, and most of the industry believes a quieter version of it.

---

# First, the theory

Every strange decision in this story traces back to one belief, so let's get it on the table. The CTO believes a developer's role is to translate specification into code. That's the whole job, in this view: not design, not judgment, translation.

The fuller worldview, as it was relayed to me: any software system can be described completely as behaviors, entities, and solutions. A behavior describes an action; a solution describes how the action happens. Write those down precisely enough and the code follows mechanically. "The code is simply an artifact of processing the spec." And if code is an artifact and translation is what developers do, the conclusion arrives right on schedule: the goal (stated openly, more than once) is to not need developers at all.

It's tempting to stop there and point. I want to do the opposite, because the cartoon version of this argument ("CTO drinks the AI kool-aid, fires the engineers") is easy to beat, and beating a cartoon proves nothing. The real version deserves better.

So here's the real version. Code is getting cheap. Not free, but cheap enough that regenerating it has started to compete with maintaining it. Specs are the durable artifact. They describe what the business wants, in language the business can read. Every team alive has felt documentation drift away from the code it describes; spec-driven development, taken seriously, doesn't manage that drift, it abolishes it. The spec is the source of truth, the code is compiled output. If the pipeline is reliable, you get software that is always documented, always regenerable, re-targetable to whatever framework wins next year. Serious people are building toward exactly this, and the tooling is real and improving.

There's also a version of this that already works, because I've seen it run. Teams I work with spec a slice, build it, and revise the spec with whatever the build taught them: spec-first with the feedback loops kept in. Those practitioners would read this story and wince, not object; nothing that follows lands on them.

And this company is arguably the best possible test case for the stronger claim. A greenfield rebuild of an existing product: known domain, a running reference implementation, no requirements invented from thin air. Payroll and invoicing: rules-heavy, deterministic, the kind of software that might genuinely be mostly specification. If spec-everything-first works anywhere, it should work here.

So I'm not going to argue with the theory; I'm going to show you the practice. I won't pretend to be neutral about it, but I will keep what he told me separate from what I make of it, so you can decide for yourself at what point the theory stopped surviving contact with it.

---

# The practice

Here's how a company produces a million lines of markdown in five months. (I had him run the count, for the record. "A million" is rounding, but not by much, and the solutioning adds more every day.)

There are two teams. The larger one "solutions" all day: they open Claude, and Claude gives them a problem to work on, usually with a yes-or-no set of answers to choose from. Pick one, next problem. Each of these conversations is private: one person, one Claude. Hold that thought.

The specs themselves come from a separate pipeline, and it is exactly one step after another: a skill reads the clickable prototype and describes every page in words; a second Claude session takes those descriptions and authors the behaviors; the humans approve what comes out. That's the assembly line. The daily yes-or-no work is the humans working their stations.

The smaller team is building the harness, the machinery that will eventually read the whole spec repo and emit an application. That's the plan for the code: not written, *processed*. Spec goes in, app comes out, November 1st.

What about tracking all this work? Not Jira; that was banned early on – there was a push on the team to use it, and leadership overruled it. Jira is the old way of doing things. The new way: every morning, Claude generates a queue of work for each person. Is the queue right? Is it in the right order? Nobody knows. Nothing exists that could answer.

The rest of the project-management layer lives in the spec repo itself, mostly in a single flat file: `backlog.md`. Bug list, work queues, change logs, all in one file, no format. Some lines have statuses, some don't. Some have dates, some don't. The only practical way to find out what's in it is to ask Claude. Let that one settle: the org's record of what is broken and what is done exists in a form that requires an AI to read. They banned the tool whose entire job is structured statuses and dates, then reinvented it as prose only a model can parse.

There is a Jira board, for what it's worth. It's empty. The stakeholders, meanwhile, have been told the team is sprinting to November – one sprint, five months long, contents to be determined.

---

# What's in the million lines

A spec is only as good as what it's derived from. This one has two sources.

The first is the old app. Early on there was a push to soak up all the existing behaviors: point Claude at the current system and extract what it does. Sensible, except the old app is poorly documented and has plenty of bugs, and an extraction pass can't tell a feature from a defect. To an observer, a bug *is* a behavior. So the bugs came over as behaviors. Requirements now, with their own spec entries. The one artifact that could have anchored the whole project to reality (years of production usage, every edge case paid for) got photographed instead of studied, warts included.

The second source is a prototype. The UX designer built a clickable mockup in React: no backend, just browser storage faking persistence so the pages feel connected. A prop, in other words – and a perfectly good one, for its intended audience of humans who understand what a mockup is. Claude was not that audience. Remember the pipeline: the behaviors are authored from Claude's verbal descriptions of the pages. Nowhere in that chain does anything know the prototype is pretend. So the prop's mechanics became requirements, and that is how a payroll system's spec came to say, in multiple places, that payroll data should be pulled from the browser's cache.

This is the part I promised we'd get to, and I want to be precise about what happens next: nothing. No human is positioned to read that sentence and laugh; nothing in the pipeline questions it, because the whole ideology is that the spec is the truth. These defects stay until someone stumbles across them. My source fixes the ones he finds; when he asked Claude to hunt for more, it found two, and a manual grep turned up a few others. Several were in the spec's own bug list. The error tracker has the error.

And when a decision does need making, sometimes nobody makes it. Architecture decisions live in the repo as ADRs (Architecture Decision Records, in name anyway, since no one reviews or approves them). One records that money will be stored as integer pennies. The actual requirement is precision to hundredths of a penny. Claude decided pennies; the decision is canon; the spec, as written, now contradicts its own requirements about money. Not because anyone chose wrong, but because the process contains no moment where a human sees the choice – the decision was written, committed, and inherited by everything downstream, the way all the decisions are.

---

# "Claude says it's correct"

Five months of output, headed for a November deadline. And remember the bet: if code is just an artifact of processing the spec, then the spec's correctness is the whole product. So the obvious question is the only question: how do they know the specs are right?

My source has asked. He gets two answers. The first is that Claude says it's correct. I'll walk through that slowly. Claude authored the specs, from descriptions Claude wrote, about a prototype that was never real. Claude assigns the work of refining them and interprets the file that tracks their defects. And when the question of correctness comes up, the authority consulted is Claude. Even process improvement is Claude: when a defect slips through, a Claude skill (it's called retro) is supposed to update the process. Not everyone runs it. The system is grading its own homework at every level, and the default grade is a pass. Doubt exists in this system, but it has to be summoned by name: ask Claude to hunt for defects and it finds them; don't ask, and the answer is yes.

> The system is grading its own homework at every level, and the default grade is a pass.

The second answer is more honest: *we should build the system and find out what it looks like*. Which is a fine idea: build something, learn from it, adjust. That's iteration – the thing this entire methodology was designed to make unnecessary, now living inside the plan as the contingency. They rediscovered it and scheduled it last.

Except the contingency hasn't been possible, because every build attempt has ended the same way: the harness stops and refuses. It has found issues in the spec, and it was built not to guess. Notice what that makes it – the only participant in this process with a standard it can't be talked out of. Every human check was deleted or delegated; the one reviewer left that says no is the machine at the end of the line. What stopped it, concretely: a spec says the app should read from a table and display the results – and nothing anywhere writes to that table. The tenant-management feature says it owns the `/accounts` endpoint; the CRM feature is implementing it too.

Any developer will recognize these. A dangling reference. A duplicate symbol. In code, the compiler catches the first before your coffee cools, and the linker refuses the second outright. The specs sat for five months because markdown has no compiler; nothing structurally capable of disagreeing ever read them. [My friend Mike Rogers](https://sep.com/author/michael-rogers/), upon hearing this story, half-shouted that they should have a CI job that detects internal inconsistency. He's right, and notice how modest that demand is. Cross-reference checks on a repo of structured documents is a lint job. And the twist is that they have lint: a rule set that's supposed to check the specs against conventions, things like making sure primary keys have the right type. Whatever those rules catch, agreement between documents isn't among them – the dangling table and the contested endpoint sat there until the harness tripped over them. The checking machinery exists, aimed below the failures: rules for the lines, nothing for the whole. Nobody pointed it at coherence, because that question was already answered: "Claude says it's correct."

And these are the easy defects, the mechanically findable ones. Dangling tables and duplicate endpoints are what a grep can catch. The spec for a payroll system also contains its share of wrong business logic: tax edge cases, rounding rules, the pennies problem from earlier. That's an inference, not a report, but it's the safe kind: a million unreviewed lines about payroll cannot all be right, and the pennies conflict is the one we happen to know about. Defects like that are semantic, the class of thing no cross-reference check ever sees. They don't announce themselves at build time. If nothing catches them first, they wait for a paycheck.

---

# The conversations that never happened

The `/accounts` collision is worth one more minute, because it's not random. Two features claiming one endpoint is what a design argument looks like when the argument never happens.

On a functioning team, that collision dies in a hallway. Someone says "wait, aren't you building accounts?" over coffee, or a design review catches it, or two engineers argue for twenty minutes about who owns what and somebody loses. The argument is the mechanism. Conflicts between people's mental models get surfaced by the friction of people talking to each other.

Here's my source's own diagnosis, the thing he says is his main problem: everything goes through Claude. No one collaborates. There is no discussion about features or issues outside of Claude.

Trace what that means mechanically. No one logged how the `/accounts` collision actually happened, but the mechanism writes itself. The tenant-management person asked Claude about `/accounts`, and Claude (agreeable, session-scoped, unaware of any other conversation) said yes. The CRM person asked their Claude, and their Claude said yes. Claude is infinitely patient and never says "that's not yours." Coherence across sessions was nobody's job, least of all the model's. The org chart still shows two teams; the communication graph is an asterisk: every person talking to the center, no person talking to another.

And look at what the humans were left to do in those conversations. The solutioning team's day is answering yes-or-no prompts. Whatever you think developers are for, this org kept them around for the one thing its own theory says they're not needed for – judgment – and then [handed them a format where judgment can't operate](https://sep.com/blog/ai-code-gen-tools-need-human-developers-to-produce-good-code/). You can't notice the table nothing writes to from inside a multiple-choice question. Noticing that takes a view of more than the question in front of you, and nobody has that view anymore; the design lives in a million lines no one has read.

The formal checks that would catch this don't exist here – there's no code to review, no design review to convene – and the informal ones have nowhere to live: every channel where one person's doubt could reach another person routes through a system trained to be helpful.

---

# The reflex

Step back from the individual absurdities and one shape repeats. Every place this process should have a check (a point where someone, or something, could catch a wrong guess before it compounds), the check has been removed or handed to the same system that made the guess.

Who verifies the specs are correct? Their author. Who approves architecture decisions? The ADRs have the form of a review process and none of the function; Claude decided pennies, and no human moment existed to catch it. Who catches two teams building the same endpoint? That's what design arguments are for, and there are no design arguments, because there is no discussion outside of Claude. What's the ground truth on project state? A file with no format that only Claude can parse. Four different bottlenecks, one reflex: when a check gets in the way, delete the check – or route it through the machine, which is deletion with better UX.

The deleted checks were all the same thing at different speeds. A colleague catches a wrong guess in minutes; a build catches it in hours; a user catches it in production, expensively. Iteration is just the name for scheduling that contact early and often.

And I keep coming back to how reasonable each step must have felt. Skipping ADR review is barely a decision when the ADRs flow in faster than anyone could read them. Letting Claude answer correctness questions feels fine when Claude wrote the material and knows it best. Nobody woke up and chose chaos; they chose velocity, one locally-sensible trade at a time, and the checks were always what velocity cost. The problem is that the checks were never the impediment. They were the process working as intended, each one a place where the work met reality. Delete enough of them and you're still moving fast – just with no way left to know in which direction.

> The checks were never the impediment. They were the process working as intended, each one a place where the work met reality.

In September, the company hired a new project manager. Her first week, she did what project managers do: asked everyone for their current Jira ticket, what's left, and time remaining, so she could build the sprint plan. Then at standup she asked which features were done and shipped. Someone had to explain it to her. There are no tickets. Nothing is done. Nothing has shipped. She listened to the whole thing – the spec repo, the harness, the November date – and delivered the review this post has been building toward:

"Who does that in 2026?"

---

# Waterfall didn't fail where you think it failed

She's asking the right question. Time to cash the check from the beginning of this post, the claim that this is a fifty-year-old failure in new tooling. Because the CTO's plan rests on a specific version of software history – one my source has heard him tell, and it goes like this: waterfall failed because turning specs into code was slow, expensive, human work, and by the time the humans finished translating, the world had moved. Under that history, agents change everything. Translation is fast now. Waterfall is back on the menu.

That history is wrong, and we've known it was wrong since before waterfall had a name. The paper everyone cites as waterfall's origin (Winston Royce's [Managing the Development of Large Software Systems](https://github.com/tpn/pdfs/blob/master/Managing%20the%20Development%20of%20Large%20Software%20Systems%20-%201970%20(waterfall).pdf), 1970) presents the single-pass, design-then-build diagram and then, in the very next breath, calls that approach "risky and invites failure." The rest of the paper is Royce adding feedback loops and arguing that you should plan to build the thing twice, because the first version is how you find out what you didn't know. The founding document of waterfall is a warning label. Everyone cites it; approximately nobody reads it.

What actually killed waterfall was never the cost of coding. It was the cost of being wrong for a long time. A big spec written up front is a pile of guesses about what users need, what the domain requires, how the pieces fit. The guesses stay unexamined until something executable meets reality. The longer the spec phase, the bigger the pile, the later the reckoning. Agile never promised faster code; it promised earlier contact with being wrong – shrink the gap between guessing and finding out.

Which is why the industry has already run this company's experiment, at scale, more than once. [My friend Jon Fuller](https://sep.com/author/jon-fuller/), reading a draft, remembered executable UML – the 2000s promise that a sufficiently precise model would generate the system. The models never stayed precise enough, and that dream retired without a eulogy. Mike again: the story reminded him less of waterfall than of offshoring. He's right that they rhyme, because [2000s-era offshoring](https://sep.com/blog/spec-driven-versus-client-satisfaction-in-outsourcing/) *drove* waterfall behavior. When communication with the people building the thing is expensive and slow, you [compensate with a Big Spec](https://wiki.c2.com/?BigDesignUpFront): write everything down, throw it over the wall, integrate at the end, and discover in the final weeks that the pieces don't fit. Whole companies learned that lesson expensively, and the problem was never the distant engineers; it was the wall. Swap the contractor for an agent and the wall is still a wall. The CTO has hired an offshore vendor with zero latency and infinite patience, one that never asks why payroll lives in a browser, and whose only pushback arrives the way the offshore wall's always did: at integration, months after the words were written.

Now run the logic forward, because this is the part that matters beyond one company in one November. If agents make spec-to-code cheap, the rational response is more builds, not fewer. Cheap construction means cheap experiments; cheap experiments mean you can afford to find out you're wrong on Tuesday instead of in Q4. Every hour agents shave off the build loop is an argument for tightening the learning loop, and this org took the exact opposite fork: they used the cheapness of building as a reason to defer building. The one resource agents made nearly free is the one they're rationing.

---

# Six weeks

So here's where they stand, as I write this. The specs are not done; solutioning continues daily. What exists contains dangling tables, contested endpoints, a currency decision that violates a known requirement, and payroll data in the browser cache. The harness refuses them. The beta date is November 1st, and even that isn't settled: ask the Chief Product Officer and the date is real; ask the Chief Operating Officer and it's aspirational. The company that believes everything can be specified has two executives running incompatible specs of the deadline.

The team's own estimate for the build, if every spec were perfect right now, is ten to thirty days of Claude cranking. Call it six weeks of runway against that estimate, and every spec is not perfect right now. Whatever margin exists is the space where they'll discover what five months of unexamined guessing produced: the phase where reality finally gets its vote, compressed into whatever's left after the first failed run.

I could be wrong about how this ends. I'd even tell you how to check: a working payroll beta on November 1st, paying real people the right amounts. If that ships, I'll write the follow-up conceding that spec-first agentic development pulled it off, and it'll be an easy post to write because I'll have learned something. They may add checks I haven't heard about: a resolution pass over the specs, a real review gate. I hope they do. But I'm not drafting that follow-up yet, because as of today the two constraints that killed waterfall haven't moved an inch. Nothing they've built has been pressure-tested against a user. Nothing they've written has been checked against anything but itself – and the one check with a hard standard, the harness, has said no every time they've run it. Everything else (the million lines, the daily queues, the solutioning) is architecture built on top of those two absences.

If you take one thing from this story, don't take "AI can't build software." Wrong lesson; the AI is the only part of this system doing its job as designed. Take the decision rule instead: when a check becomes your bottleneck, the move is to [make the check cheaper](https://sep.com/blog/verification-the-most-important-software-development-tool-in-the-age-of-ai/) – lint the specs, automate the review, shrink the batch so verification fits inside it. The moment you delete the check instead, you've stopped building software.

You're just transcribing guesses.