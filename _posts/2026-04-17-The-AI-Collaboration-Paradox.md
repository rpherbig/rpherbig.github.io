---
title: "The AI Collaboration Paradox"
layout: post
---

<link rel="canonical" href="https://sep.com/blog/the-ai-collaboration-paradox/" />

One of our teams at SEP has gone all-in on agentic development. I don't mean they're simply using AI tools heavily; I mean they're deliberately redesigning their team processes, shared infrastructure, and ways of working around it. When I was talking to the team about their experiences, one thing kept jumping out at me:

> AI development is highly collaborative. We are pairing, mobbing, and reviewing constantly. I see a direct relationship between AI usage in a team's processes and required collaboration to be most effective as a team.
> 
> —[Joe Coy, Lead Software Engineer](https://sep.com/author/joe-coy/)

I pushed back on this a bit. More collaboration, not less, were they sure? The entire team was emphatic: yes. In fact, it wasn't just that they were collaborating more. At some point, AI stopped being the thing they were figuring out and just became part of how they work. The conversations shifted from "how do we use AI" to the stuff you'd talk about on any healthy team: process, developer experience, how we work together.

That's not something the industry is talking about right now. The dominant narrative around AI-assisted development is individual throughput: ship faster with fewer people. The solo developer with an agent (or swarm) is the new unit of production. That's what the tooling vendors are selling, what the thought leaders are tweeting, what the conference talks are about. Even when collaboration comes up, it's usually human-to-AI collaboration, not human-to-human. Those claims might be true, but they're incomplete.

Is this team an outlier, or is there a pattern here I haven't been seeing?

---

# So I Asked Around...

I took the question to a few of the thought leaders in agentic development across SEP. The responses were... not what I expected.

Nobody else reported quite the same dynamic Joe described, but the reasons were interesting.

Andrew pointed out that his team has a distinctly different structure - "to each their own" when it comes to AI. No shared documents, no centralized customization, people using different tools (Copilot, Claude Code, Cursor), configured differently, solving problems differently. And in that adoption model? No increase in collaboration. He drew a direct line to Joe's team:

> Because all their AI infrastructure is shared, they have to collaborate more or risk clobbering each other's work. We don't have those risks and thus have no incentive to collaborate any more than we were.
>
> —[Andrew Dunlap, Senior Software Engineer](https://www.linkedin.com/in/andrew-dunlap-sep/)

Brian, who is on Andrew's team, reinforced this: the tool variance meant nobody bothered trying to create a shared setup. The fragmentation was actively reducing collaboration, because people could figure things out on their own without talking to anyone. If shared tooling had been a goal, he thinks it would have sparked more conversation. But it wasn't, so it didn't.

Steven, who's on a fully remote team, wasn't sure AI had changed collaboration on his team one way or the other. But he suspected that uneven adoption had increased the need to collaborate, they just hadn't prioritized it. He also surfaced a whole different problem I hadn't considered: AI-mediated communication. Some people on the team leaned heavily on AI to write their asynchronous messages to each other, which meant the receiver had to run every message through their mental "AI hallucination detection" filter. On a remote team where most collaboration is already asynchronous text, that's a real tax on trust.

Jyotsna's team uses AI, but not at the volume or autonomy level of the others quoted here. At that lower volume, she hadn't seen the same collaboration increase. But she noticed something subtler: AI had sparked more conversation between the team's tech lead, Rui, and the developers, because AI was enabling the team to move faster, and the review process needed to keep pace.

---

# What's Actually Going On?

The pattern isn't "AI increases collaboration." That's what Joe's team experienced, but it's not the whole story. The pattern is more specific: shared AI infrastructure increases collaboration. Individual adoption doesn't, and uneven adoption across a team is the worst of both worlds: increasing the need to collaborate without creating the structure to actually do it.

Joe's team built shared tooling (context files, skills, subagents, etc.), shared processes, and shared conventions around using AI. That created a forcing function - you simply can't all work in the same AI infrastructure without talking to each other. The team called it an enabling constraint, and the term fits: the shared infrastructure didn't just happen to coexist with more collaboration, it required it.

This echoes Conway's Law: the team's AI adoption model is an architectural decision, whether the team realizes it or not. Shared infrastructure creates communication pathways, whereas individual tooling doesn't, and most teams aren't making this choice deliberately. They're defaulting to "to each their own" because it's the path of least resistance. That default might be fine. But it's worth knowing it is a choice, and that it has consequences.

---

# I'm Not The Only One Noticing

I went looking for whether anyone outside of SEP was seeing something similar. Nobody is making this exact argument, but a few things point in the same direction.

[Kent Beck has been arguing](https://shiftmag.dev/kent-beck-ai-genies-are-not-replacing-developers-yet-5367/) that as AI makes implementation cheaper, the skills that gain leverage are the human ones: goal-setting, project management, breaking work into milestones, design judgment. Those are all collaborative by nature: nobody sets goals in isolation, breaking down a project requires shared understanding of the system + the team's capacity + the tradeoffs, and so on. When the bottleneck shifts from “can we write the code?” to “do we agree on what to build and why?”, that's indicative of a need for more human-to-human conversation, not less.

Thoughtworks is more direct. A recent piece on [preparing teams for the agentic SDLC](https://www.thoughtworks.com/en-us/insights/articles/preparing-your-team-for-agentic-software-development-life-cycle) calls out that faster decision-making makes "close cross-functional collaboration and mob programming essential practices." Their [AI/works podcast](https://www.thoughtworks.com/insights/podcasts/technology-podcasts/inside-ai-works-agentic-development-platform) goes further, arguing that interdisciplinary pairing (dev + product owner, dev + QA) is now almost mandatory because specs need to be complete from all dimensions.

And then there's the data from Microsoft's dotnet/runtime team. Stephen Toub [wrote up ten months of using GitHub's Copilot Coding Agent](https://devblogs.microsoft.com/dotnet/ten-months-with-cca-in-dotnet-runtime/) across 878 pull requests. One detail jumped out: CCA pull requests required 43% more review comments than human-authored ones, and a larger share needed heavy iteration. Toub himself described his role shifting from implementer to reviewer and guide, spending more time on design, architecture, and mentoring - all of which require other people.

These are different contexts and different scales, but they all end up in the same place: the more work AI handles, the more the remaining work requires talking to each other.

---

# What I'm Taking From This

The plural of anecdote is anecdata, not evidence, but the pattern holds across enough teams internally and externally that I think it's worth acting on. Most teams adopting AI are focused on the easy stuff: which tools, which models, how much code can we generate. Fewer are asking how adoption changes the way the team actually works together, and almost nobody is treating the adoption model itself as a deliberate architectural choice.

Joe's team stumbled into something by going all-in on shared infrastructure. They didn't plan for the collaboration increase - they described it as emergent. It's fair to ask whether the causation runs the other way, whether teams that already collaborate well are just more likely to build shared infrastructure. I can't rule that out. But it happened, and they're better for it. Meanwhile, teams defaulting to individual adoption aren't getting that benefit, and might not realize what they're missing. If I had one takeaway, it's this: the next time a team is deciding how to adopt AI, “shared vs. individual” deserves to be part of the conversation. Not because shared is always right, but because the choice matters more than most people think.
