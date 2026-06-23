---
title: "Custom AI vs. Off-the-Shelf: Stop Asking If, Start Asking Where"
layout: post
---

<link rel="canonical" href="https://sep.com/blog/custom-ai-vs-off-the-shelf-stop-asking-if-start-asking-where/" />

A client came to us with a clear vision: build a scheduling app for their staffing business, complete with a natural language interface so managers could describe scheduling constraints in plain English instead of wrestling with a GUI. They knew exactly what they needed custom AI for.

They were wrong.

Custom AI is software built for your specific problem. Off-the-shelf AI is an API or product you buy: something that already exists, and in 2026, it covers more ground than most teams realize. As it turns out, natural language interfaces are basically a commodity now.  We sketched out the architecture together, pointed out where a little prompt engineering and a well-chosen API would go a long way. Sprinkle in some evaluation & a dash of monitoring, and you're cooking. They got it, and they walked away without a custom AI engagement.

Then they came back. The scheduling optimizer, the part they figured they had covered, was where commodity solutions fell flat: the naive algorithms were too slow, and the schedules they produced weren't good enough to use. That's where they actually needed us.

---

# What 'Off-the-Shelf' Actually Covers Now

Here's the thing about off-the-shelf AI in 2026: it's genuinely remarkable at some things and remarkably bad at others. The problem is that the line between those two categories keeps changing, and it's not obvious on which side a given problem lands.

Natural language interfaces? Largely solved.

Image recognition? Pretty much solved for common objects (still hard for specialized domains).

Summarization, classification, extraction, basic reasoning? [Mostly solved](https://crfm.stanford.edu/helm/), with caveats: even the best models [still fail tasks that are straightforward for humans](https://arcprize.org/arc-agi/2).

Combinatorial optimization? Scheduling under complex constraints? Domain-specific prediction on sparse data? Still hard. [Custom software & AI hard](https://sep.com/case-studies/global-sawmill-equipment/). Sometimes even "call your friendly neighborhood ~~Spider-Man~~ PhD" hard. (For reference: [Google's own production scheduling still runs on classical solvers](https://developers.google.com/optimization), not LLMs)

The most common mistake we see isn't "they tried to build something they should have bought", it's "they assumed the hard part was the part that looked unfamiliar", and the unfamiliar parts are often what commodity AI has gotten good at.

---

# Two Projects, Two Surprises

We've run into the reverse just as often. An architectural firm came to us with a need to detect certain objects in blueprints. The traditional approach is to use Computer Vision. We'd compare algorithms for this specific use case, account for rotation & orientation & skew, artifacts from the scanning process, occlusion (elements overlapping), etc. Don't forget building a labeled dataset (potentially by hand). And then a pipeline to make it repeatable as we gather more data, adjust the training process, etc. A real project with real custom software & AI.

We could have done that. We have in the past. But this time we reached for a Vision-Language Model instead. None of that complexity was a problem. A little code to handle some details and domain-specific quirks, and it worked well enough: it hit a level of accuracy where reviewing and fixing its output was faster than having a person do the whole job from scratch. The conversation shifted from "can we build this?" and "how much will it cost?" to "is it worth going further?".

---

# Six Questions to Ask Before You Build or Buy Custom AI

The teams that got into trouble made the build-vs-buy call before they fully understood the problem. Here are the questions worth asking first:

1. **Have you decomposed the problem?** "We [do/don't] need custom AI" is rarely true of an entire system. For example, the staffing app needed commodity AI in one place and custom AI in another. Treat each sub-problem as its own build-vs-buy decision. Decomposing the problem pays off in other ways: the more specific the problem, the easier to evaluate AI's performance and improve it if needed (and the more likely we are to find a pre-existing solution!).

1. **Can you define success precisely?** Think "we need this piece to do Y, and we'll know it's working when Z." If you can't answer that, you can't evaluate whether any solution, custom or off-the-shelf, actually works.

1. **Are there constraints that eliminate the question?** Security, regulatory, legal, and IP constraints are a category unto themselves - if any of these apply, they often make the decision for you. If that's your situation, [Jordan Thayer wrote a thorough breakdown of exactly that](https://sep.com/blog/when-to-reach-for-custom-artificial-intelligence-solutions-vs-off-the-shelf/).

1. **What does good enough look like?** Off-the-shelf solutions often get you to a high baseline cheaply. Sometimes that's fine! Sometimes it's not - e.g. if your use case requires 99% accuracy and the baseline is 80%. Know which situation you're in before you commit. Have those conversations with stakeholders early.

1. **Has anyone solved this exact sub-problem before (to that level of "good enough")?** The more specifically the existing solution matches your specific problem shape, the better the result and the faster to identify success or failure. "Has AI been applied to our industry?" won't cut it.

1. **Is there a cheap way to find out?** At some point, conversation and research must give way to experimentation. [A focused feasibility effort](https://sep.com/case-studies/ai-road-planning-software/), before any significant commitment, can answer questions that no amount of architectural discussion will resolve.

---

Custom vs. off-the-shelf isn't really a single decision: it's a series of smaller ones, made at the sub-problem level. The practice that most influences success is resisting the urge to answer the question before you've decomposed the problem.

If you're weighing this decision, [talk it through with someone who's been on both sides](https://sep.com/services/ai/).
