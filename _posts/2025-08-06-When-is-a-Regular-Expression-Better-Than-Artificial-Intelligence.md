---
title: "Speaking: When is a Regular Expression Better Than Artificial Intelligence?"
layout: post
---

## Given at

* dev up Conference 2025
* KCDC 2024: [Slides](https://www.dropbox.com/scl/fi/jurrdwhz4owhqmidok807/When-is-a-Regular-Expression-Better-Than-Artificial-Intelligence_-KCDC-2024.pdf?rlkey=t278mw9znl1g4xjnt4ugploy9&st=wfbra18c&dl=0)
* CodeMash 2023
* Indy.Code() 2022

## Abstract

Natural language processing is a technique for taking human understandable text and wresting machinable information from it through a variety of techniques.  When we think about NLP, we typically think about tasks like assessing the tone of a passage of text, answering questions stated in natural language, or summarizing a large amount of text.  We recently helped a client build a system for scoring pre-interview screening assessments using AI & ML. 

Typically, we spend a great deal of effort trying to convince our clients that there are AI techniques relevant to their problems, and that those approaches are mature enough for prime-time use.  Here, I had the opposite problem: the client knew AI was appropriate for their problems, and they were absolutely convinced it was ready for deployment.  However, they wanted to use AI to solve all of their automated scoring problems.  Over the course of building the system, I found several situations where simpler non-AI techniques could provide comparable or better performance than state of the art AI.

In this talk, we'll discuss:

* Why automating scoring was a fundamental business need for our client
* What their technical approach to automated scoring was
* How we improved their existing AI models
* How we identified situations where AI wasn't the best approach

By the end of the talk, the audience will:

* Have been introduced to several models for AI-based natural language and code understanding
* See a 10,000 foot view of how to automate scoring rubrics for assignments that include both programming and human communication
* Have some rules of thumb for deciding when AI is necessary or when a simpler technique is likely to exist or be more desirable.

## Tags

## Description of target audience

The target audience are people in positions of technical leadership on a project.  Specifically, both those that are trying to sell the adoption of newer technologies within an organization, and those that are trying to push back on the over-adoption of a new technology.

Our talk will also go (briefly) into the gory details of a system that uses AI as part of its process.  This will likely interest developers that are interested in AI for its own sake as well as product owners looking to see what they can expect when incorporating AI into their products.
