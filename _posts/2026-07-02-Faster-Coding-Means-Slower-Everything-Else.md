---
title: "Faster Coding Means Slower Everything Else"
layout: post
---

<link rel="canonical" href="https://sep.com/blog/faster-coding-means-slower-everything-else/" />

At some point in the last year, my work changed: I was spending more time reviewing code than writing it. I can't point to the moment it happened, there was no process change, no deliberate decision... I just looked back at the last year and noticed what had happened.

Once I noticed it, I started asking around. Were other people feeling the same shift? Yes! Engineers across SEP agreed (as SEP's *AI Practice Lead*, I get to see this from across teams and client conversations, which is what made the pattern hard to miss). Rachel Harness said she didn't think reviewing had gotten slower, it was just proportionally more of what she did. Craig Belcher said he spends most of his time reviewing now; and while he doesn't love it, he's adjusting to a new normal.

That got me curious about what the research says. And the research, it turns out, is a mess:
* [GitHub's study](https://arxiv.org/abs/2302.06590) showed developers are 55% faster with Copilot. But that's 55% faster at **completing a single coding task in a lab**. It didn't measure review time, integration, or whether the feature could have actually shipped.
* [METR ran a randomized controlled trial (RCT)](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/) and found experienced open-source developers were actually 19% *slower* with AI tools, while believing they were 20% faster.
    * Though the sample was small, the codebases were unusually mature, and [METR themselves have since partially walked it back](https://metr.org/blog/2026-02-24-uplift-update/).
* [Faros AI tracked telemetry from 10,000+ developers](https://www.faros.ai/blog/lab-vs-reality-ai-productivity-study-findings) across 1,255 teams. Individual output was up: 21% more tasks completed, 98% more PRs merged. But those are development-done metrics, not features-shipped. **DORA delivery metrics at the organizational level stayed flat**. Review times increased 91% and PR sizes grew 154%. More code got produced. It didn't get out the door faster.
    * [Their 2026 follow-up, now covering 22,000 developers](https://www.faros.ai/blog/key-takeaways-from-the-dora-report-2025), found the trend **accelerating**: PR review time up 441%, and 31% more PRs merging with no review at all.
* [Stephen Toub documented the same dynamic](https://devblogs.microsoft.com/dotnet/ten-months-with-cca-in-dotnet-runtime/) across 878 PRs over ten months on the dotnet/runtime codebase: one engineer with AI assistance can **generate review demand faster than teams can absorb it**.

So which is it? Are we faster or slower at shipping features?

As a consultant, I'm obligated to say "it depends". But in this case it really does! It depends on what we measure, and nobody's measuring the same thing.

---

# The Theory of Constraints (TOC)

There's a concept from manufacturing called the Theory of Constraints. The core idea is simple: every system has a bottleneck, and improving anything that *isn't* the bottleneck doesn't improve the system. It just moves the pressure. If the factory floor can stamp 1,000 widgets per hour but quality inspection can only handle 500, buying a faster stamping machine gets you a bigger pile of uninspected widgets. We didn't get faster, we got a more impressive backlog.

> Every improvement not made at the constraint is an illusion.
>
> –[Eliyahu Goldratt, The Goal](https://en.wikipedia.org/wiki/The_Goal_(novel))

Applied to software: for most experienced teams, writing code was never the slow part. My colleagues Chris Shinkle, Brian Hanford, and Andrew Dunlap [made this case in a recent webinar](https://sep.com/events/beyond-code-gen-rethinking-ais-role-in-software-development), citing DORA data showing developers spend as little as 8% of their time actually writing code. Understanding requirements, making design decisions, coordinating across components, reviewing each other's work, validating & accepting features... that was where the time went. AI tools made the *already relatively fast* part faster. So the pressure moved to everything downstream. And the downstream steps didn't get faster. In some cases, they got harder.

This is a Theory of Constraints problem, and the general principle is worth stating: relieving one constraint doesn't eliminate constraints, it just exposes the next one.

---

# Where's the Next Constraint?

What does the next constraint actually look like? "Maintaining quality" is the easy answer, but it's too vague to be useful. Here are the specific failure modes I'm seeing:
* **The volume shift**. This was the most consistent thing I heard. Not that individual reviews got harder, but that there's just *more reviewing to do*. Wes Hoffman put it well: "I don't think reviewing and verifying code are slower or harder. I do feel like there is more code to review more often." When we can generate code in minutes that used to take days, the review queue fills up faster than review capacity grows.
* **Larger changesets**. The Faros AI data puts a number on this: PR sizes up 154% among AI-adopting teams. Multiple engineers I talked to confirmed the trend. It's natural with AI tooling to make bigger changes and therefore bigger code reviews, but Brian Hanford pushed back, and I think he's right to: "This is a process problem. Just because you can, doesn't mean you should." We can have AI break work into smaller chunks, but that takes intentional effort.
* **New categories of bugs**. Joe Coy shared a story that stuck with me: AI generated a complete test suite, perfectly structured, good coverage... except the class under test was a mock. The tests were testing themselves! That's just not a mistake a human would make. Review intuition built from human error patterns misses an entirely new class of AI-specific failure modes.
* **Architectural drift**. AI is remarkably good at getting individual functions right while [missing the bigger picture](https://dev.to/vuong_ngo/ai-keeps-breaking-your-architectural-patterns-documentation-wont-fix-it-4dgj). Naming conventions drift across generated files. Data flow patterns that should be consistent aren't. Design decisions that would be a one-line statement in a design doc become invisible when spread across 90 files of generated code. Locally correct, globally incoherent.
* **The testing squeeze**. Ryan Schade shared that a large pharmaceutical client had been calling because their testers couldn't keep up with dev teams anymore. That's the bottleneck shift at enterprise scale. Charles Penn, Senior Test Engineer, raised the deeper question: "How much do we want to let our AI test our AI?" It's not just philosophical. Research on AI-assisted code review has found that LLMs exhibit [confirmation bias](https://arxiv.org/pdf/2603.18740) when reviewing AI-generated code, and AI testing tools remain largely in pilot phases with [limited demonstrated benefits](https://www.qable.io/blog/is-ai-really-helping-to-improve-the-testing) in production. The correlated error problem is real: the same blind spots that produce a bug can miss it during review.
* **Unconscious trust**. This is the most subtle failure mode on the list. Joe Manley was honest about it: "I probably have taken a lighter approach with these PRs because, in the back of my mind, I know that AI has helped." This is [automation bias](https://atomicrobot.com/blog/ai-review-fatigue/) at work: research has found that erroneous automated advice gets followed at a 26% higher rate when automation is involved, and that providing AI-generated review as a starting point actually makes human reviewers *worse* because they anchor on what the AI flagged and miss issues elsewhere. The presence of AI in the process can actually reduce scrutiny. That's backwards!

---

# How Teams Are Responding

Part of why most teams haven't acted is that the most common metrics (PR count, cycle time, lines of code) all say everything is fine. No, better than fine, they're going up! Those measure the throughput of the fast step, not the health of the constraint. There's a deeper argument about which metrics actually matter in [an AI-assisted workflow](https://sep.com/blog/the-workflow-that-teaches-itself-a-self-improving-agent-workflow/), but that's a separate post.

The most common response I heard was using AI to cope with AI's output: running e.g. Copilot reviews alongside manual review, using AI to summarize changes and focus attention, etc. This is pragmatic, probably a net positive, but it's not a structural change. It's adding AI to the review step the same way it was added to the code writing step.

Some teams have gone further and I want to highlight their innovations:
* Rui Liu's team inserted a new step between the ticket and the code: a solution design document. The design doc captures schema changes, API surface, business logic in pseudocode, and data flow. It gets reviewed *before* anyone writes a line of code. The result: when a 7,000+ line change lands across 90+ files, reviewers aren't reconstructing intent from generated code. They're verifying code against a stated design. Problems that would be buried across dozens of files are one-line statements in the doc.
* Joe Coy's team formalized an agentic review process, maintained as infrastructure they version and iterate on, followed by a live mob review with a structured agenda: demo of functionality, review of changes to shared agents and skills, code highlights, and findings from the agentic reviews. This didn't come from a top-down redesign of their process; rather it emerged from wanting to move faster and finding out that humans still needed to be meaningfully involved.
* Steven Mills needed to test large refactorings on a legacy codebase and was spending too much time on manual regression testing. He invested in a BDD-style (behavior-driven development) testing framework built around a DSL (domain-specific language) that defines legal user actions. The team bootstrapped the core patterns and wrote documentation for the AI on how to extend the DSL. Now the AI writes tests, but only within the vocabulary the humans defined. Review becomes simpler: if the test uses the DSL correctly, it's probably fine (and the test code is extremely readable, so problems are easy to notice). If the AI modified the DSL itself, it needs a good reason. If it touched production code during a test-writing task, something went wrong, so more scrutiny.

The humans are creating structure and enabling constraints so the AI can operate within them. The investment is upfront and architectural, not reactive: instead of reading code and trying to figure out what it was supposed to do, reviewers are checking whether it matches what was already decided.

---

# Where This Goes

The pattern is clear: speeding up code generation moved the constraint to review, QA, and acceptance. That's not a failure of AI tools, that's just how all systems work: if we relieve one constraint, the next one surfaces. This specific bottleneck (review and verification) is today's constraint, but it won't be tomorrow's. Teams will adapt, tools will improve, and the bottleneck will move again.

The teams that navigate this well will be the ones that developed the instinct for spotting the next constraint before it becomes a crisis. That's not a tool choice or a process tweak, it's discipline and awareness. This is a snapshot in time, not a conclusion. The tools are changing fast, the evidence and practices are early, and the teams I've talked to are still figuring it out. If you've seen this bottleneck shift on your team, or found a way to work around it that I haven't covered, I'd love to hear about it. Reach out!
