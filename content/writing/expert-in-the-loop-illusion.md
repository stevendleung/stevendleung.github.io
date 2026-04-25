---
title: "The Expert-in-the-Loop Illusion: Why Agentic AI Feels Closer to Production Than It Is"
date: 2026-04-25
description: "There's a massive gap between using AI agents as a domain expert who can course-correct, and building agents that work for everyone. Most teams underestimate this gap."
tags: ["agentic-ai", "context-engineering", "ai-safety"]
author: "Steven Leung"
draft: true
---

There's a pattern I keep seeing in agentic AI, and I think it's catching a lot of teams off guard.

You build an AI agent to help you with a task you know well. You're the domain expert. You prompt it, it does something, you catch the mistakes, refine the approach, and over time you develop a workflow that genuinely accelerates your work. It feels like magic.

Then someone says: "This is great. Let's ship it so everyone can use it."

And that's where things fall apart.

## The feedback loop you don't notice

When you use an AI agent as a subject matter expert, you're providing something the system can't provide for itself: continuous, implicit course-correction.

You notice when the output doesn't look right, not because the system flagged it, but because you know what "right" looks like. You adjust prompts mid-conversation based on intuition. You know which results to trust and which to double-check. You fill in the gaps the agent leaves without even thinking about it.

This creates an illusion. The agent feels highly capable because the combined system (you + the agent) IS highly capable. But the agent alone is not.

<!--
TODO: Add a specific example from your experience here.
Something like: "When I built [the detector research agent], I could steer it through ambiguous research tasks because I understood the data and the domain. But when I considered making it available to other team members who didn't have that same context..."
-->

## What breaks when you remove the expert

When you try to productize an agent-powered workflow for non-expert users, all of that implicit course-correction disappears. The system now needs to:

- **Recognize its own uncertainty.** You used to catch bad outputs. Now nobody's watching.
- **Handle ambiguity without a human intuition backstop.** You used to resolve ambiguous situations by applying domain knowledge. The agent has to either get it right or know when to ask.
- **Fail gracefully, not confidently.** The worst failure mode isn't a crash. It's a plausible-looking wrong answer that the non-expert user trusts.

<!--
TODO: Add another specific example. Maybe from the consulting work?
"When I built an AI-powered operations system for a small business, the challenge wasn't the AI capabilities. It was designing the system so that someone without my technical background could tell when the AI was wrong..."
-->

## This is a knowledge transfer problem, not an engineering problem

Most teams treat the gap between "works for me" and "works for everyone" as an engineering problem: better prompts, more guardrails, more testing. And those help. But the core challenge is knowledge transfer: how do you encode the domain expertise that made the expert-in-the-loop version work into a system that doesn't have that expert?

This is harder than it sounds because much of the expert's contribution is tacit. You don't know what you know until the agent gets it wrong and you think, "Obviously that's not right." But "obviously" is doing a lot of work in that sentence.

## What this means for agent safety

This gap has direct implications for AI safety. If we can't reliably build agents that operate safely without expert oversight for business workflows, how confident should we be about deploying agents in higher-stakes environments?

The answer isn't "don't deploy agents." It's to be honest about where we are: agentic AI is a powerful tool for augmenting experts, and a risky one for replacing them. The gap between those two use cases is where the hardest problems in agent reliability, safety, and trust live.

<!--
TODO: Consider adding a closing thought connecting this to your broader interest in AI safety/security. Something brief that ties back to your work.
-->
