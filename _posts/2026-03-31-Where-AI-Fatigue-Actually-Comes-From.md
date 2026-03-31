---
title: "Where AI Fatigue Actually Comes From"
layout: post
---

<link rel="canonical" href="https://sep.com/blog/where-ai-fatigue-actually-comes-from/" />

If you've spent time with agentic development, you've probably felt that particular flavor of mental exhaustion that hits harder than the work seems to justify. I wasn't stuck on a hard problem. I wasn't debugging something gnarly. I was just… keeping up. And then suddenly I wasn't. Steve Yegge calls this [the AI Vampire](https://medium.com/@steve-yegge/the-ai-vampire-eda6e4f07163): the energy drain is real, even when the output is good.

There's a growing narrative that explains the why: AI amplifies your decision load. More agent output means more things requiring your judgment, more decisions per hour, and [your brain buckles under the volume](https://forge-quality.dev/articles/quality-cost-of-ai-vampire). It's a clean story. It makes intuitive sense.

But I don't think it's right.

I've been working with and interviewing teams that are deep into agentic workflows. These are different teams with different workflows, running multiple agents in parallel across real products in different industries, not just side projects. When I asked them directly, they confirmed the fatigue, but consistently said they weren't making more decisions per hour than before AI tools. The fatigue is real. But it's not coming from where people think.

---

# What I Expected vs. What I Found

I went in expecting to hear that AI had reshaped the decision landscape – maybe not "10x more decisions", but at least a noticeable increase. What I heard instead was far more interesting!

The micro-decisions are mostly gone. Nobody's agonizing over variable names, import ordering, or the right way to structure a for loop. The AI (or even a linter!) handles that, and it's good enough at it that you don't think twice. What remains (and what arrives faster) are the macro-decisions: architecture calls, product tradeoffs, "should we even be building this?". Those were always there, you just used to have hours of implementation work between them – now you don't.

> This sort of feels like software engineering without the programming. There's still plenty of problem solving, coordinating, product thinking, testing strategy, etc. It's just at a different level of abstraction.
> 
> —[Brian Ball, Staff Software Engineer](https://sep.com/author/brian-ball/)

There is one new category of cognitive work: managing the agents themselves. Tuning prompts, watching for hallucinations, building new skills, figuring out why an agent went sideways. That's real overhead that didn't exist before, but nobody I talked to pointed at it as the thing draining them. It's a new skill to develop, not a treadmill.

The consistent pattern was: roughly the same number of meaningful decisions, shaped differently. So if it's not the decision volume, what's actually causing the fatigue?

---

# Where's the Fatigue Actually Coming From?

Three things kept coming up in my conversations, and they're all related.

1. **The natural recovery time is gone.** Compile times, manual implementation, waiting for CI, etc. None of that was "productive" in any traditional sense, but it was accidental recovery time: low-intensity work that let your brain relax between the moments that require real judgment. AI collapsed that gap. You can go from one architecture decision straight into the next product tradeoff with nothing in between. It's easy to hit your cognitive ceiling faster, not because there are more decisions, but because there's no room between them.
2. **Every output carries a trust tax.** When you write your own code, you know what you intended. When an agent writes it, every piece of output comes with an implicit "…is this actually correct?" That verification cost is small per instance but constant; it's background cognitive load that didn't exist before.

> There's that added layer of agent performance, staying vigilant to spot hallucinations and avoid automation fatigue. Every piece of data comes with added doubts – ‘is this actually correct?' – which is fatiguing.
> 
> —[Steven Kneisler, AI Engineer](https://sep.com/author/sjkneisler/)

<ol><li value="3"> <strong>And the big one, present in every conversation I had: parallelization becomes the default.</strong> Say an agent is working on something and I have 20 minutes before I need to review its output. What do I do? I spin up another agent on a different task. Now I have two streams. Then three. This is what the industry recommends – maximize your throughput, keep every cycle busy. One person I talked to described it as a "togglable state" – constantly diving in and resurfacing across multiple workstreams, with no real "heads down" time left. Nobody makes a conscious decision to work this way. The freed-up time is just there, and filling it feels productive. But every additional stream is a context switch, and context switches are where judgment quietly degrades.</li></ol>

---

# It's the Context Switching

The fatigue pattern everyone I talked to described comes back to the same thing: filling every gap AI creates with more parallel work, until the context switching is what's draining you – not the decisions themselves.

The temptation is natural. AI frees up time, and leaving that time empty feels wasteful. But running three agent streams because you can manage three is different from defaulting into four because the time was there. You know the feeling when your reviews get shallow, when you start approving things you haven't really read, when you're reaching for the next context switch before you've finished the current thought. That's your ceiling. Don't push through it – that's where the expensive mistakes live.

So what do we do if we're not aggressively spinning up more work?

> Our implementation workflow takes a couple of hours to run. Early on the question came up: what's the best use of that time? The answer we've landed on: pay attention – not multitasking, not disengaging. Document what you notice: code smells, unexpected agent decisions, requirements that seem off. Those notes feed directly into the next step, where an agent cross-references your observations against its own findings and surfaces improvement suggestions. Staying present during the workflow has become one of the most valuable things a developer contributes.
>
> —[Joe Coy, Lead Software Engineer](https://sep.com/author/joe-coy/)

What Joe's team figured out is that the time AI frees up isn't wasted if you spend it observing rather than producing. That's a fundamentally different default than "spin up more agents" – and it's one that protects the judgment that makes the rest of the work worth anything.

None of this is a new framework. Decision fatigue, [automation bias](https://cset.georgetown.edu/publication/ai-safety-and-automation-bias/), [sustainable pace](https://agilealliance.org/glossary/sustainable-pace/), Pomodoro – these are known concepts. The useful move isn't renaming them with "agentic" in front. It's applying them honestly to a context where there has never been more pressure to overload yourself.

The fatigue is real. The cause is simpler than people want it to be.
