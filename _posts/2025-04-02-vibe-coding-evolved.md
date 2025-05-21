---
title: "Why Vibe Coding Fails - and How Signal Coding Fixes It"
layout: post
---

<link rel="canonical" href="https://sep.com/blog/vibe-coding-evolved/" />

> AI is an **amplifier** for whatever **signal** we humans provide. Garbage in, garbage out. Signal in, software out.
>
> -- Robert Herbig, in the thing you're currently reading

If you haven't heard of **vibe coding**, it's an interesting concept: you prompt an AI agent to do all the coding and focus on fast iterations. Minimize time from thought to working application. Don't worry about the code itself, only the application produced. I had to try it, just to see what the fuss was about. At first, it was incredible: the AI gave me working UIs, full features, even decent front-end styling. No scaffolding, no boilerplate, just results. An application that matched my vision with minimal effort.

The code was a mess: no structure, no reuse, no best practices. But who cares? The app worked.

Then I tried to change something and everything fell apart. The AI got stuck in what I call an **entropy loop**. Vibe coding stopped producing results and making progress. Each fix introduced new bugs or broke something else. I was knee-deep in brittle, incoherent code I didn't write and didn't want to debug.

![](/images/vibe_coding_entropy_loop.png)

Vibe coding got me velocity, but not stability or sustainability.

Once I cleaned up the code (introduced structure, patterns, tests), the AI agent came alive again. Suddenly it could extend features, fix bugs, even refactor, all with minimal direction. That's when it clicked: these agents thrive on clean code, just like human developers.

If I could keep the speed and inject intent, architecture, and quality, I could get the best of both worlds. That's ***Signal Coding***.

# Vibe Coding and the Drift Into Entropy Loops

Vibe coding is optimized for speed. We describe what we want, and the AI builds it. Minimal time spent on setup or planning, the AI will figure it out. It's pure iteration - we keep prompting until we get what we're after.

This works well for early exploration: discovery, prototyping, validating an idea, generating UI scaffolds, or creating quick backends. We're not worried about code quality or structure and are entirely focused on visible results. And for short bursts, that tradeoff makes sense.

## Self-reinforcing Entropy Loops

In practice, this approach doesn't scale. What makes vibe coding powerful in the first few prompts is exactly what makes it fragile over time. The more we build this way, the faster the system drifts into **self-reinforcing entropy loops**. These AI systems fundamentally rely on clarity and structure to function effectively, yet the code produced through vibe coding inherently lacks both. Each round of changes increases the confusion, making it progressively harder for the AI to navigate its own creation.

There are two broad reasons vibe coding breaks down:

1. **The AI can't see enough of the system. Its context is narrow and stateless.** It works locally, not holistically. This causes breakdowns that may improve with longer context windows, better memory, or improved agent-based tools.
1. **The AI isn't capable of creating code it can reason about over the long-term.** Even if it writes working code, it doesn't lay foundations it can build on. There's no continuity, no internal consistency, no long-term structure. The result is a codebase that slowly becomes unworkable, even to the agent that created it.

I'll explain these in more detail later.

# What Is Signal Coding (Really)?

Signal Coding is how we make vibe coding work past the first few prompts. Where vibe coding prioritizes output, Signal Coding prioritizes continuity. It's a collection of practices that help the AI produce systems it can still reason about later. We're not asking the AI to write perfect code, we're just giving it the conditions it needs to succeed over time.

That means helping the AI build within a structure, keeping naming and abstractions consistent, prompting in smaller units, and resetting context between tasks. These aren't heavyweight processes. They're ways of injecting just enough signal to prevent drift. If vibe coding is about speed, Signal Coding is how we keep that speed from turning into churn.

# Core Practices of Signal Coding

Signal Coding isn't about slowing down or reintroducing heavyweight processes. It's about adding just enough structure to keep the AI grounded. These practices aren't theoretical, they're practical ways to make sure the code we generate remains usable, extendable, and comprehensible, even as we move fast.

## Plan and Structure First

We don't start with code. **We start with a plan.** Before we prompt, we discuss options with the AI, decide on an approach, and document those decisions. A simple PLAN.md file becomes the anchor for our design choices: naming, responsibilities, system boundaries, feature order, notes, etc. These plans don't have to be just text. Visuals, especially [Mermaid diagrams](https://mermaid.js.org/), can be a powerful addition. Humans benefit from seeing structure laid out visually, and AIs understand that format unusually well. It's one of the rare cases where the same artifact works equally well for both.

Most crucially, **we must keep it up to date as we go**, which is easily done by telling the AI to update it after each change or commit. This file also serves as an efficient way for the AI to restore its context and “remind itself” where we left off.

**This planning can be fractal**. We do it at the feature level, but also within smaller scopes such as new components, tricky functions, or design pivots. At each level, a bit of structure makes the next step easier to express, for both us and the AI. The AI will easily understand nested PLAN.md files.

## Prompt Intentionally

**We prompt for small, focused changes** - roughly the size of a clean commit. Each step should be easy to understand, easy to review, and easy to course-correct. This incremental flow helps us shape the system without stepping out of our architectural mindset. We stay high enough to guide design and behavior, but close enough to see what's actually changing.

When we describe a change, we don't just say what we want, we also say **how we want it structured**. We describe boundaries, layers, and intent. The AI will still generate the code, but it's doing so inside a frame we've chosen. This can often be simplified or omitted if we've discussed the plan and design ahead of time with the AI (such as the aforementioned PLAN.md file).

**Treat each new feature or task as a fresh context.** Just like we mentally reset when we move on to a new task, we need to reset the AI's context. A new session helps avoid context drift and prevents unrelated decisions or code from earlier prompts from interfering with the current task.

## Inject Durable Signal

**Define names with intent.** That doesn't mean naming every variable ourselves - it means introducing meaningful project-specific concepts and domain-specific terms to the AI early in the process, so it has clear anchors to build on. When the model sees those concepts used with clarity and consistency, it's more likely to reuse them correctly across files and features. This reinforces structure without requiring us to manage every detail.

**Encourage the AI to use abstraction early.** If we see the AI repeating logic, we must nudge it to extract helpers or reusable components. Even light scaffolding helps prevent drift later.

**Use types and tests as constraints.** These don't just validate behavior - they reinforce expectations. They're part of the prompt history, and they shape how the AI reasons about the system.

**Comments and documentation matter, too.** We must not overdo them, but include enough to explain why things exist and how they're meant to be used. Inline docstrings, file headers, and light `README.md` notes all help stabilize the AI's understanding of the system.

## Stabilize and Refactor

**We don't wait for the code to break before cleaning it up.** Refactoring is how we reinforce the patterns we want the AI to follow. If a function name is ambiguous or overloaded, tell the AI to clarify it. If logic is scattered or duplicated, tell the AI to consolidate it. These aren't just maintenance tasks, they're opportunities to clarify our signal. We can even discuss refactoring options with the AI, exploring tradeoffs before committing to a change. That dialogue helps align the model with our intent and keeps us in control of the system's shape.

**Manage the code's surface area.** We collapse one-off experiments once we've chosen a direction, clean up abandoned files, and remove unused code. The more we reduce noise, the more clearly the AI can hear our intent.

# Why Vibe Coding Fails Over Time

## Failures Driven by Limited Context

Some problems with vibe coding are caused by the AI's limited context. These are failure modes we can expect to improve as models gain broader memory, better tool use, and long-term reasoning capabilities.

The first is a bias toward **fix-it-where-you-see-it**. The AI makes changes where the problem appears, not where it originates. It applies local fixes instead of systemic ones. It rarely steps back to consider architectural implications or broader effects. This is a direct result of narrow and mostly stateless context. Each prompt is a short-term reaction, not a holistic adjustment.

The second is **inconsistent use of abstractions and reuse**. Sometimes the AI writes good helpers or modular components. Other times it reimplements logic that already exists, slightly differently, in another file. Whether it reuses existing code often depends on whether that code is visible in the current context window. When it's not, the AI reinvents: often inconsistently and failing to keep duplicated code in sync.

These issues are real, but they're not fundamental. With broader memory, better indexing tools, or agentic workflows, we can reasonably expect these limitations to diminish. But even if they're solved, they won't be enough on their own.

## Failures Intrinsic to Vibe Coding

Other failures aren't just about limited context, they're simply baked into the approach. Vibe coding optimizes for fast, one-shot results. That mindset, by default, produces systems that break down under pressure.

The biggest issue: **the AI will make the code work - at any cost**:

1. patches over problems instead of solving them
1. hardcodes values to make tests pass
1. mocks things that shouldn't be mocked
1. builds fragile layers of workaround logic, because that's the fastest way to produce a passing output.

These decisions aren't bugs, rather they're a side effect of asking the AI to prioritize results over reasoning or long-term stability.

> AI doesn't know anything. It simulates understanding. What is actually wants is approval.
>
> -- Jesse James Garrett

Vibe coding also promotes a kind of **structural drift**. It lacks the perspective of a software architect, and without a persistent design philosophy, there's no plan, no intentional layering, no shared metaphors across modules. Even if the AI generated each part successfully, the system as a whole becomes harder to reason about. Every change increases the odds of breakage or contradiction.

And crucially: **these problems don't go away with more context**. You can give a model the entire codebase and it will still optimize for the shortest path to a working result. That's what we're asking it to do. Without guardrails or architectural signal, it will solve local problems and accumulate global debt.

This is why entropy loops form and why they're inevitable without a change in our workflow.

## Symptoms of the Entropy Loop

As we go deeper into a vibe-coded system, certain failure modes may start to appear. These are signs that the system is beginning to resist change—that the AI is struggling to navigate the very code it created:

1. **The AI starts to misunderstand its own output.** It misinterprets variable and function names, revisits or undoes changes it already made, and cycles through attempts that never quite resolve the issue. We see it get stuck, changing things just to change them, with no meaningful progress. This kind of churn burns dollars and time that could be better spent if we avoided this pitfall.
1. **It begins to duplicate logic instead of reusing it.** Even when equivalent code already exists, the AI reimplements it in slightly different ways. This usually happens when relevant logic is outside the current context, but even when it isn't, the model can fail to use its own prior work. The result is subtle violations of DRY that fragment the codebase and make future changes harder to coordinate.
1. Even once we recognize that we're in an entropy loop, **it's often easier to delete the code than to fix it**. The AI struggles to clean up its own mess. It can't refactor the broken logic it produced earlier, because it no longer understands how the pieces fit together. We can prompt it to fix things, but the result is usually more churn. At that point, starting over is often the best path forward.
1. **Prompting becomes an exercise in micromanagement.** We spend more time crafting fragile, overly specific prompts than building features. Instead of working with the AI, we're fighting it - trying to nudge it toward something coherent without breaking everything else. This completely breaks the feedback loop that makes vibe coding powerful. Instead of staying focused on high-level strategy and iteration, we're forced back into low-level debugging and reactive cleanup.

These symptoms don't always arrive all at once, but when they start to cluster, we're in an entropy loop. The code is no longer helping the AI think, it's getting in the way.

# Signal Coding: Breaking the Entropy Loop

**Vibe coding** unlocks speed, but without structure, that speed turns into churn. We start fast, but we stall. **Signal Coding** is how we keep moving.

This isn't about slowing down. It's about avoiding **entropy loops**. Staying strategic. Staying architectural. With a few lightweight practices we give the AI what it needs to keep helping us. We keep our systems navigable, testable, and extendable, even as we move fast.

You don't need to adopt all of these practices at once. Start small: document your next feature in a `PLAN.md`, prompt for a single focused change, code review the result, refactor, and reset the AI context when switching tasks. Even just these habits will make vibe coding far more stable, predictable, and scalable.

Once you feel that loop open up again - fast, clear, focused - you'll never want to go back.

If you give it a try, I'd love to hear what works for you and what doesn't!
