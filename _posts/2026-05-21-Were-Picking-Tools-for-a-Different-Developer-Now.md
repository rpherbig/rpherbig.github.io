---
title: "We're Picking Tools for a Different Developer Now"
layout: post
---

<link rel="canonical" href="https://sep.com/blog/were-picking-tools-for-a-different-developer-now/" />

A colleague of mine, Joe Coy, recently told me something that stuck with me. His team had chosen Maestro over Appium for mobile UI testing. The team's reasoning made a lot of sense: Maestro was lightweight and easier to set up. By every traditional measure, it was the right call.

Then they started using an AI agent to write and maintain those UI tests. The agent hallucinated constantly! Maestro's documentation was thin enough that the model didn't have reliable patterns to draw from, so it made things up. The tool that was easiest for humans to use turned out to be the hardest for the agent to use.

Joe put it simply: "AI doesn't care about setup complexity - it likely would have handled all that heavy lifting with Appium for us. What it does care about is having good training data."

What does that mean for how we pick tools when the agent is doing most of the typing?

I think it means the evaluation criteria are shifting. Product fit is still the primary constraint - the tool has to solve the actual problem. But agent fit is a factor that didn't used to exist, so we need to change our thinking.

---

# What actually makes a tool "agent-friendly"?

My first instinct was "popular tools are agent-friendly tools." And that's... partially true. Popularity correlates with training data, which correlates with the agent generating reliable code. But popularity is a proxy, and it turns out to not be a great one. A tool can be wildly popular and still trip agents up if it has three coexisting major versions with different APIs. A niche tool with a tiny-but-crystal-clear interface might work better.

I talked to a bunch of colleagues and dug into what practitioners are actually experiencing:

* **Training data footprint**. Has the agent seen enough usage of this tool to generate correct code? [Simon Willison has written](https://simonwillison.net/2025/Mar/11/using-llms-for-code/) about deliberately choosing libraries with this in mind - favoring stable, well-established options specifically because they'll be well-represented in training data. He frames it as [Choose Boring Technology](https://boringtechnology.club/) applied to AI-assisted development: innovate on your product's unique selling points, stick with tried-and-tested options for everything else. The more examples of a library that exist in the training corpus, the less likely the agent is to make things up.

* **Documentation quality**. Not just 'do the docs exist' - we've all seen auto-generated docs that helpfully inform us the `name` parameter holds the name. It's whether the docs are clear, complete, and structured enough for an LLM to actually learn from. This is what burned Joe's team: Maestro had documentation, but it was thin enough that the agent couldn't build reliable patterns from it.

* **Version coherence**. This one keeps coming up. Libraries with multiple coexisting major versions create a specific kind of failure: the agent will confidently blend patterns from v2 and v3 in the same file, even when you explicitly tell it which version to use. I've experienced this myself - asking for v3-compliant code and getting v2 idioms mixed in, or vice versa. Joe Coy's team had to reinforce their Swift version across multiple agent configuration files before the errors stopped. Sasha Kotlyar hit something similar with an SDK and fixed it by explicitly pointing the agent at the documentation root for the correct version.

There's a silver lining here too. Keith Hanson told me that agent hallucinations around a library actually created pressure to upgrade to a newer major version. The upgrade was already on the team's radar but low priority - until the agent kept generating code that assumed the newer version's API, and the team realized the newer version was where they should be anyway. The agent's bias toward the newer version turned out to be a useful nudge, not a hallucination to work around.

* **Text-composability**. Can the tool be driven entirely through code, config, and CLI? Or does it require visual interaction or manual setup steps that an agent can't easily perform? Brian Hanford hit this wall with JetBrains' DotTrace - he wanted to feed profiling results to an agent for analysis, and the tool had no textual export path (the data was locked behind a GUI). Jyotsna Raghuraman independently flagged CLI support as something she actively looks for. This is a factor I haven't seen anyone else writing about yet, but it might be the most straightforward one on the list: the agent can either interact with the tool's output or it can't.

Those four have real stories behind them. The next two I'm less certain about - they make sense to me logically, and nobody's pushed back on them, but I don't have a "we got burned" anecdote yet:

* **API surface clarity**. A consistent, predictable interface versus one full of special cases and implicit state. [Anthropic's engineering team has found](https://www.anthropic.com/engineering/writing-tools-for-agents) that simpler tool interfaces outperform broad endpoint wrappers when agents are the consumer. That's about MCP tool design, not library selection, but the principle likely transfers.

* **Human maintainability**. Can the team still read, debug, and own what the agent produces with this tool? Everyone I talked to agreed this matters. Nobody had a story of getting burned by it yet. I suspect those stories are coming.

---

# When you can't change the tool, change the scaffolding

Sometimes the tool is chosen for you. Jyotsna Raghuraman pointed out to me that her choices are often dictated by client constraints - she picks the tool first, then finds the best agent workflow around it. That's reality for a lot of us. So what do you do when you're stuck with something agent-unfriendly?

Andrew Dunlap works with NVIDIA hardware and bleeding-edge open source models where training data is sparse and docs are thin. His workaround: build local documentation as you go. Errors, failure states, success cases, etc. are all captured as reference material that compensates for what the ecosystem doesn't provide. Sasha's version-root anchoring and Joe's prompt reinforcement are lighter-weight versions of the same idea, the kind of deliberate investment in our workflow I wrote about in [Treat Your AI Workflow Like You Treat Your Code](https://www.rpherbig.com/2026/05/06/Treat-Your-AI-Workflow-Like-You-Treat-Your-Code.html). These workarounds work, but they're extra effort - effort we wouldn't need if the tooling were agent-friendly in the first place.

---

# Don't overcorrect

It would be easy to read all of this and start optimizing entirely for the agent. Don't.

> Can you imagine explaining to a stakeholder that the software can't do something because you picked a library the AI works well with, but that doesn't actually support the product's needs? Maybe that's a contrived scenario, but I don't want to have that conversation either.
>
> —[Andrew Dunlap, Senior Software Engineer](https://www.linkedin.com/in/andrew-dunlap-sep/)

A few things to keep in mind:

* **Agent fit is a tiebreaker, not the deciding factor**. When two tools both solve the problem, agent-friendliness is the thing that should tip the decision. When only one tool solves the problem, use that one.

* **Don't ignore what your team already knows**. If your team has deep expertise in a framework and the agent is marginally better with something else, the maintenance cost of switching probably isn't worth the generation speed you'd gain.

* **Popular doesn't mean agent-friendly**. It's a correlation at best. Don't use GitHub stars as a proxy for how well an agent will work with a library.

* **Don't treat today's criteria as permanent**. Models are getting better fast. The gap between "popular tool with lots of training data" and "niche tool with great design" will likely shrink. A library that's agent-unfriendly today might not be in a year. This whole post is a "right now, today" observation, not a law.

---

# This is bigger than your next pull request

But here's what won't go away: the idea that our tools need to work for agents, not just humans. Tool vendors are going to start getting evaluated on whether their products can participate in agentic workflows - whether they can be scripted and consumed by an agent as easily as by a human, stable versioned APIs, structured documentation. That's not a library selection question anymore, that's a product development question, and the vendors that figure this out first will have an advantage that has nothing to do with how usable their GUI is.

There's one more question worth pondering, courtesy of Andrew Dunlap: why don't we just write the library ourselves? Agents lower the cost of rolling your own solution significantly. We definitely still want external dependencies for the hard stuff: authentication, cryptography, security, database drivers, dependency injection. But the calculus of "add another dependency vs. build" is shifting, and for simpler libraries, the answer might be different than it was two years ago.

I wrote this article not because I have a complete framework, but because every conversation I had about it surfaced something new. If you've got a story about tool selection in an agentic world, I'd love to hear it.
