---
title: "Everybody Agrees You Should Hire Junior Engineers. Almost Nobody Does."
layout: post
---

<link rel="canonical" href="https://sep.com/blog/everybody-agrees-you-should-hire-junior-engineers-almost-nobody-does/" />

A colleague, Charles Penn, asked me recently what I thought the future looked like for junior engineers. He’s someone who always keeps the human element in view, and he’d been reading the same things I had. Juniors wondering out loud whether they’d be unhirable in a few years. Companies saying the quiet part out loud: *why hire a junior when AI produces a rough approximation of their work?* It was an excellent conversation and I didn’t have a satisfying answer.

Around the same time I talked with a CS professor. His college had planned for a class of six hundred and change; meaningfully fewer showed up. His own program, computer science and software engineering, expected well over a hundred new students. Fewer than half that number arrived. Not because students stopped liking computers. Because they and their parents had been reading the same posts, and “software engineer” had started to look like a risky bet instead of a sure one.

Put those together and you get a fear that compounds. Juniors afraid there’s no seat for them. Companies quietly deciding not to offer one. And the next class looking at all of it and choosing a different major entirely.

---

# Agreeing is the easy part

Here’s the strange part: the argument for hiring junior engineers has already been won. Should you hire junior engineers in the age of AI? Yes. Nearly everyone who has looked hard at the question agrees. The gap is in the doing.

Microsoft’s Mark Russinovich and Scott Hanselman [made the case](https://dl.acm.org/doi/10.1145/3779312) that cutting juniors while leaning on AI collapses the pipeline that produces your future seniors. Stack Overflow’s blog spent a top-ten post of the year [mourning the entry-level path](https://stackoverflow.blog/2025/12/26/ai-vs-gen-z/) and still landed on the same conclusion: no juniors now, no seniors later. Andrew Murphy [put it more bluntly](https://andrewmurphy.io/blog/ai-didnt-kill-your-junior-pipeline-you-did): nothing about AI forces a company to stop hiring juniors. The pipeline collapse is a choice. It isn’t only engineers saying so, either. Even a Brookings economist [makes the same case](https://www.brookings.edu/articles/borrowed-expertise-why-ais-productivity-boom-may-not-survive-the-generation-that-built-it/) from the outside. Even the doom pieces agree on the fix. Ask almost anyone in engineering leadership whether the industry *should* keep developing junior engineers and you’ll get a yes.

Now look at what the industry is doing. A [Stanford analysis of payroll data](https://digitaleconomy.stanford.edu/publications/canaries-in-the-coal-mine/) found employment for the youngest software developers (ages 22 to 25) fell nearly 20% from its late-2022 peak, while older cohorts held steady or grew. The students noticed: CS enrollment just posted [the steepest decline of any major in the country](https://builtin.com/articles/computer-science-degree-decline-ai), per National Student Clearinghouse data.

So the interesting question isn’t “should you hire junior engineers?” That one’s settled, at least out loud. The interesting question is why almost nobody acts on the answer, and what it takes to be a firm that does.

I work at one. I lead SEP’s AI practice, which means my day job is watching what these tools can and can’t do. SEP has hired six to nine new-grad engineers every single year through the freeze, 2020 to 2026. Not as charity, and not because we didn’t hear about AI. Because we did the math differently. The rest of this post is that math, with our own numbers attached.

---

# The trick is, we hire them earlier

Reg Braithwaite (a.k.a. Raganwald) has a line I’ve never been able to improve on: [“We only hire senior developers. The trick is, we hire them earlier in their careers.”](https://social.bau-ha.us/@raganwald/116617915437809248) His longer version: senior engineers are what you get when you hire a junior, give them interesting problems, surround them with people who know more than they do, and wait.

That’s the whole bet. Juniors aren’t a cost center we tolerate or a charity program we run. They’re the supply chain for engineering judgment, the asset a consulting firm lives or dies by. Buy it on the open market and you’re renting from a labor pool everyone else is also draining and nobody is refilling. Make it yourself and you own the means of production.

Ok Rob, that’s a bit grand. But the plain version holds: our seniors have to come from somewhere, and “somewhere” is either a plan or a hope that some other company keeps training them for us.

When I put the industry’s logic (*juniors write the simple code, AI writes simple code now, so no more juniors*) to Kyle Pinches, [SEP’s Director of Talent Acquisition](https://sep.com/blog/why-we-look-for-pd-when-hiring/), he didn’t fight the premise. “The part that is wrong is what isn’t said. ‘Juniors write the simple code’ is true but incomplete.”

Incomplete how? Start with the part you can watch on any of our teams this week: juniors ask questions. Kyle’s list: “why did you do this this way?” in code reviews. “Why does our codebase look like this?” while pairing. “Why is this bigger than I thought?” in sprint planning. Sometimes the question reinforces what the team knows. Sometimes the team changes how it does things. Sometimes it surfaces a corner case everyone else has grown blind to. And in our experience, people this early in their careers are capable of really serious work, with mentoring and guardrails around it. That’s not “simple code,” and it isn’t waiting eight years to pay off, either.

The fuller answer is the rest of this post. But fair warning: before I make our case, I’m going to make the other side’s, because the case for not hiring juniors is better than most of its defenders realize, and pretending otherwise is how you end up writing a recruiting brochure instead of an argument.

---

# The case for not hiring juniors is better than you think

Let me make the other side’s argument properly, because the version that circulates (“AI writes code now, so who needs juniors”) is a cartoon, and beating a cartoon proves nothing.

For decades, junior engineers earned their keep on a particular kind of work: boilerplate, CRUD endpoints, test scaffolding, small well-bounded bug fixes. That work had a beautiful property: it was simultaneously *useful output* and *the work a junior learns on*. The company got working code; the junior got reps. The economics of junior hiring rested on that two-for-one.

AI didn’t take the junior’s job. It took the two-for-one. The learn-on-it work is now near-free, which means a junior’s early output is worth less than it was in 2019, while the cost of growing them stayed the same or went up. The ramp didn’t disappear; it just stopped paying for itself along the way. Software isn’t even the only profession watching this: law firms are living the same math, with the due-diligence grind that once taught young lawyers contract law [now compressed to minutes](https://www.slaw.ca/2026/07/31/the-hidden-economics-of-the-vanishing-apprenticeship/).

I watch this happen up close. When I interview our newest engineers about how they use AI, the handoffs are real: Logan Cover had a parser to build for a mock server, recognized it as a well-defined problem, gave the whole thing to AI, and saved a day and a half. He was right to. That’s the learn-on-it work, leaving.

And the ramp was never cheap to begin with. The visible cost is a salary. The real cost is senior attention. Dante LaRocca, a Staff Engineer here who typically leads the technical direction on his teams, estimates that around half his week goes to what looks like mentoring: answering questions, explaining decisions, talking through implementations with the engineers around him. At a consulting firm, the ledger says senior hours are the product. Every hour spent leveling someone up has a billable rate attached to the alternative – a skeptic reads Dante’s number and sees a measurable senior tax.

Then there’s the exit problem. A junior crosses into clearly-net-positive somewhere around the two-year mark, which is precisely when a company that *didn’t* pay for their ramp can offer them 30% more, because it saved the training budget you spent. Train, lose, subsidize a competitor. Every firm that’s been burned this way has a name and a face in mind.

And the consulting-specific kicker: clients don’t love paying for someone’s education. A senior-only roster is easier to staff, easier to sell, and easier to defend in a pricing conversation.

One more, because it’s the newest and least discussed: there’s a real worry that AI is making juniors *worse*: that a graduate who leaned on a model through school arrives with atrophied fundamentals, having skipped the productive confusion where understanding forms. If that’s true, the ramp isn’t just unsubsidized now. It’s longer.

That’s the case, and it is locally rational at every step. If your planning horizon is a fiscal year, it might even be correct.

The catch is in the phrase “planning horizon,” and in a few things the argument doesn’t say out loud.

---

# Why we do the math differently

Start with the objection that sounds most damning for a consulting firm: clients don’t want to pay for someone’s education. True, they don’t. They also don’t have to. [Our teams are deliberately blended](https://sep.com/blog/what-its-like-to-work-at-a-software-consultancy/): juniors and seniors structured together, juniors billed at lower rates than seniors, senior oversight on the same invoice. The client gets supervised work at a competitive blended price. Nobody is paying tuition disguised as consulting. And the development happens *inside* real client work, not in some training annex we eat as overhead (and eventually pass on to a customer). That last part matters more than it sounds: it means the mentoring isn’t a program we fund. It’s a property of how the teams are built. Raman Ohri, our CEO, is blunter about the economics: “in practice, the delta between time to get a junior ready and time to hire and integrate a senior is much smaller than most would expect, if you have the infrastructure in place”.

Which reframes the senior tax. Remember Dante’s number, that half of his week spent on questions and implementation talk. Here’s what I left out: that’s not time diverted from his job as a technical lead. That *is* his job as a technical lead. The same hours that level up the engineers around him are the hours where he shapes the technical direction of the project. And it runs both ways, he notes. The junior engineers often know specific corners of the system better than he does. I asked several of our senior engineers what mentoring costs them, expecting a number. Mostly what I got back was polite rejection of the question. Robert Uhl, another Staff Engineer, put it flattest: on paper the company loses a couple of billable hours a week to [the formal program](https://sep.com/blog/why-we-mentor-at-sep/), and “beyond that it’s almost impossible to disentangle the investment in mentorship from the daily work.”

When the people paying the tax can’t find it on their ledger, maybe it’s the ledger that’s wrong. It’s also only half a ledger. Uhl finds mentoring keeps his own learning skills sharp and pulls him into topics he’d never have found on his own. Teaching makes the teacher better too.

The consulting model hides a growth dividend. Chris Halvorson, a Staff Engineer who [started here as a junior](https://sep.com/blog/my-year-as-an-apprentice-software-engineer/), points to the project variety: coming up to speed on new domains again and again, with support, is what taught him to find parallel patterns across languages and systems. A product company gives a junior one codebase to go deep on. We give them a tour through many. It’s a generalization engine, and generalization is judgment’s raw material.

And the atrophy worry, the one I called newest and least discussed? Take it seriously and notice what it indicts: leaving a junior alone with an answer machine. If unstructured AI reliance erodes fundamentals, then the throw-them-at-the-ticket-queue model of junior development is what just died, and [deliberate mentorship](https://sep.com/blog/apprenticeshipmentorship-success/) (the kind where someone flags the lesson in the moment and checks that you learned it) got more valuable, not less. Whatever walks in the door, development is the variable a firm controls. That’s the part everyone cutting juniors is also cutting.

But you shouldn’t take my word for any of this, or theirs. Take the numbers:

![Retention by hire year cohort chart](/images/retention-by-hire-year-cohort.png)

The flight-risk objection, measured: about 76% of our new-grad cohorts are still here at three years, and 58% at five. That’s a full year or three past the point where the steelman says they take the money and run. Some do leave. The ones who leave are the honest cost of the model, and these numbers already include them.

And of the new grads who stay six or more years:

![New grads reaching senior roles chart](/images/new-grads-reach-senior.png)

(The other 5%? Still here and still climbing.) Kyle doesn’t find that number surprising, which took me a second to appreciate: “My job is to hire juniors that I have high expectations for.” He hires expecting exactly that outcome. The 95% is the plan working.

David Mott has been that plan since 1995. He started as a junior; at some point someone on the management team mentioned he was [their model for a senior engineer](https://sep.com/blog/what-does-it-mean-to-be-a-senior-engineer/). Not a senior, *the model*. He figured he should probably accept it. The lessons his mentors flagged for him back then weren’t syntax: “Figure out what the client actually thinks is important, even if they don’t actually say it.” Thirty years later that’s still the curriculum, and notice what it’s made of. Client-reading. Context. Judgment. The part AI didn’t eat. Halvorson describes his own crossing the same way: one day his job had become explaining, designing, delegating, sitting with clients in tricky technical situations. Nobody’s typical day is “write the boilerplate” anymore. Theirs never was going to be.

The juniors see the line too. Kate Mikels saw AI chase a build failure down a rabbit hole of confident, irrelevant fixes when the actual cause was a dependency server being down, a fact no model in her editor could see. Knowing when the answer isn’t in the code. There’s no prompt for that.

So here’s the bet, stated plainly:

![Current engineers who started as juniors chart](/images/current-engineers-started-junior.png)

Except that when I asked Raman about the decision to keep hiring through the freeze, he declined to make it sound like a bet at all. “We saw no compelling reason to change a strategy that had worked for decades,” he told me. The market never stopped paying for junior engineers on blended teams; our ability to get them up to speed never broke; so nothing changed. He pointed out something the current panic conveniently forgets: the industry was reluctant to hire and invest in early-career engineers *long* before AI. It was a community talking point all through the 2010s. The aversion is old; only the excuse is new. These days the move has a name: AI-washing.

He also gives the other side more credit than most people arguing for juniors do. Stop hiring juniors, keep the hiring bar, buy seniors instead (assuming you can), and “we would likely be an even more capable engineering powerhouse – in the short term”. But the difference, he thinks, is small, the juniors adapt to new ways of working as fast or faster, and the real costs show up elsewhere: higher turnover, less internal innovation, less of the energy that fuels [hackathons](https://sep.com/blog/how-we-run-company-hackathons/) and community work. Stop hiring juniors and the damage doesn’t appear where you’d expect, in some future staffing gap. It appears in your *seniors*, in what their jobs stop containing. In eight years the missing bench (six of every ten seats, if our history holds) is just the part you can count.

Raman notes one more thing the buy-seniors plan glosses over: mishires. You can miss on a hire at any level, but in SEP’s experience it happens more with seniors. Hiring a good senior is harder than hiring a good junior. A senior arrives with habits and assumptions you have to deprogram, then reprogram to your culture; a junior learns your way of working from the start. And the truly exceptional engineers are very hard to find on the open market once they’re senior. Our retention numbers are part of the reason why.

Maybe the market proves us wrong. Maybe seniors stay cheap and plentiful and the poachers eat well forever. We’re not betting they won’t, simply out of contrarian conviction, we’re just refusing to break a machine that works because of a LinkedIn meme.

---

# Whose job is this, anyway?

One more thing before the decision rule, because it’s the part of this whole discourse that bothers me most. Nearly all the advice in the “AI and juniors” conversation is aimed at the juniors. Level up. Learn the tools. Differentiate yourself. Adapt or be replaced. The kid gets the homework; the industry gets a pass. But a junior can’t mentor themselves, can’t staff themselves onto a team with people who know more than they do, can’t structure their own eight years. The one thing every voice in this post agrees on (the mentors, the mentored, the guy who runs hiring, the guy who signs off on all of it) is that turning juniors into seniors is the *firm’s* job. It was our job before AI, and it still is. AI just gave everyone a better excuse to quit doing it.

So if you run an engineering org and you’ve been nodding along while your entry-level requisitions sit at zero, here’s the rule I’d offer: cutting juniors doesn’t save the money. It defers the bill eight years and adds interest. You’ll pay it back in senior-market prices, in a market you helped thin out. And if the honest reason is that your company never built the machine for turning juniors into seniors, then AI isn’t your reason. It’s your cover story. Building the machine is the actual work. It’s also entirely buildable. Ours isn’t magic, just structured teams, [deliberate mentorship](https://sep.com/blog/apprenticeshipmentorship-success/), and the patience to let Raganwald’s “wait” actually run.

Robert Uhl said something when I asked him about mentoring that I haven’t been able to stop thinking about, so I’ll just leave it with you:

> “I’ve benefitted from the shade of the trees planted by those before me and I want to make sure that the forest is there for the next generation.”

Somebody planted your seniors. Plant some of your own.
