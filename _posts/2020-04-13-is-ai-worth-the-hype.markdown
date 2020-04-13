---
title: "Is Artificial Intelligence Worth the Hype?"
layout: post
---

<link rel="canonical" href="https://www.sep.com/sep-blog/2020/04/13/is-ai-worth-the-hype/" />

![](/images/Gartner_Hype_Cycle.svg)

*Image courtesy of Jeremykemp at [English Wikipedia](https://commons.wikimedia.org/wiki/File:Gartner_Hype_Cycle.svg) / [CC BY-SA](https://creativecommons.org/licenses/by-sa/3.0)*

In [Everyday AI Problems](https://www.sep.com/sep-blog/2019/10/10/accidentalai/), my colleague [Jordan Thayer](https://www.sep.com/sep-blog/author/jordan-thayer) said the following:

> When someone asks me "What can AI do for me?", I often suspect the answer is
> "Not much" because it's the wrong question. If someone asks me "Is there a way
> to make this free text machinable?" or "Are there better techniques for
> scheduling these work orders?" the answers are "Yes!" and "Almost certainly."
> Are the techniques that solve those problems AI? Absolutely.

Is AI worth the hype? Absolutely. Jordan believes this so strongly that he
pursued a doctorate in it and dedicated his entire professional career to it.
I'm a bit late to the party, but I agree with him and am trying to make up for
lost time! That said, AI isn't a panacea; just because something is worthy of
the hype doesn't mean that individual deployments can't fail because they're a
misapplication or just a bad idea overall. In the following, let's discuss:

* What is AI?
* When should you use it?
* When shouldn't you use it?
* So what hype _is_ justifiable?

## What is AI?

Artificial Intelligence is getting a computer to do anything that would otherwise
require a human. [Common applications](https://www.sep.com/sep-blog/2019/10/10/accidentalai/) include:

* [Machine learning](https://en.wikipedia.org/wiki/Machine_learning)
* Planning and scheduling
* Game playing
* [Machine vision](https://en.wikipedia.org/wiki/Machine_vision)
* [Natural language processing](https://www.sep.com/sep-blog/2019/11/29/several-examples-of-nlp/)

While the machines are trying to imitate human capabilities, the way they do
that is often quite alien. Consider asking an AI and a person each to tell you
whether or not a tweet expressed a positive or negative sentiment about a
topic. The person would read the tweet, understand its meaning, and give you
an answer.

In stark contrast, many AI approaches to sentiment analysis won't even try to
understand the text as a whole. Instead, they look at the distribution of
words in the tweet, the length of those words, and the amount of punctuation
used. This statistical analysis allows the AI to reliably predict the
sentiment of the text without needing to produce a deeper understanding.

It's important to keep the difference in approach in mind. While AI can do
things that we typically think of as requiring a human touch, they do so by
different means. Our tendency to anthropomorphize things works against our
intuition here. An application of AI doesn't think in the conventional sense.
Its outputs are the result of common processes in mathematics, computer
science, and engineering being rigorously applied to some problem of interest.

## When is AI Appropriate?

AI comes up in situations you might not think of, or in ways differently than
you might imagine. For example, AI happens a lot in industrial settings from a
controls perspective: to solve a large constraint problem to ensure that we
don't put an oil refinery in a dangerous configuration. [This drone
application](https://www.technologyreview.com/s/608811/drones-and-robots-are-taking-over-industrial-inspection/)
complements it: use drones to view hard-to-reach elements of an industrial
facility to reduce the cost of manual inspection.

If your project fits within these guidelines, it's a good candidate for AI:

* It can be thought of as requiring a human.
* You can describe it through a rigorous or formal process.
* It has a solution that is right/wrong or good/bad.
* The human cost of completing it is significant.
* The machine cost of completing it is less than the human cost.

Some [problems that you encounter every
day](https://www.sep.com/sep-blog/2019/10/10/accidentalai/) fit those
criteria, and are often solved using artificial intelligence:

* Scheduling constrained resources (classes in classrooms, meetings in meeting rooms, participant availability)
* Planning sequences of actions
* Predicting the next element in a series based on the previous elements
* Identifying elements in a picture
* Building a summary of a large body of text

## When is AI not the right answer?

AI is not the right tool for every task. It is important to remember that
artificial intelligence will not replace human intelligence.

* Does your task require a process to be adaptable to unforeseen circumstances? If you cannot predict the workflow for the task, and it takes a human to make nuanced decisions, the task is not suitable for AI.
* Is the human cost negligible or [the compute cost prohibitive](https://www.technologyreview.com/s/614700/the-computing-power-needed-to-train-ai-is-now-rising-seven-times-faster-than-ever-before/)? If AI will not save your company at the bottom line, then it is not worth your time developing the AI.
* Can you define your task formally? AI follows strict rules — do or do not; it cannot make decisions, create on the spot, or think out of the box. If you cannot provide those rules to make your program work, it's not a good candidate for AI.
* Do societal norms prohibit automation? In some cases, an AI can completely replace a job previously done by a human. There is a [great fear that automation will make humans obsolete](https://www.genesys.com/podcast/series/take-a-moment/ai-ethics-an-inside-look-at-the-future-of-artificial-intelligence). How does society ensure those people can continue to provide for their families? If we find that an AI can completely drive a car, will the passengers trust it? How does insurance and fault work in the event of a crash?

## Justifying the Hype

[This reality](https://en.wikipedia.org/wiki/AI_winter) means that we may
never see [Robby the Robot](https://en.wikipedia.org/wiki/Robby_the_Robot) or R2-D2 or Data. They are relegated to the realm
of science fiction with flying cars. AI is often silently in the background,
playing a large role in many industries that directly impact our everyday
lives. Here are some absolutely game-changing examples:

### Greenhouse Logistics

Cultivating crops with higher yields that are more resilient to the elements
and pests is a problem whose solution affects all of us - after all, everyone
needs to eat! Here, AI is being used to reduce the human effort required for
phenotyping.

Phenotyping is the study of plant characteristics, like the size of the fruits
they produce, under various conditions. Large-scale phenotyping used to be
time and labor intensive - a human made the observations by hand. Scientists
developed machine vision algorithms to do it for us.

Further, the AI planning community has been using [automation of smart
greenhouses](https://www.bosch.com/stories/greenhouse-guardian-ai-in-agriculture/)
as a benchmark domain for a decade. The logistics problems that 'crop up' here
are moving plants (or equipment) to:

* Control the amount of light, water, and nutrients each plant gets
* Pass the plant beneath a variety of sensors

### Medicine

Medicine has advanced dramatically in the last century thanks in no small part
to advances in medical imaging. Medical imaging provides information that is
critical to determining what is going on with an individual so that the proper
course of action can be determined.

Medical imaging is an excellent domain for deploying machine vision
algorithms. In particular, deep learning has been [remarkably
successful](https://www.radiologytoday.net/archive/rt0118p10.shtml) in
reducing the time between a first consultation and a diagnosis and increases
the number of patients that can be treated by each doctor. This is also a
great example of how AI works best with human collaboration.

## Conclusion

It's easy to get excited about AI. There is so much progress made in so many
fields which all show the promise of AI. Although we must be realistic about
the scope of AI, we can still get excited about its prospects.

[We must be unafraid to
fail](https://www.aninews.in/news/business/businesses-gaining-value-from-artificial-intelligence-experimentation-mindtree-study20190912114211/).
In the end, all AI deployments are an experiment, because we can't know
upfront how well a technique will work for a set of problems that we've never
seen before. Failing, understanding, and iterating is a huge part of
developing AI solutions.
