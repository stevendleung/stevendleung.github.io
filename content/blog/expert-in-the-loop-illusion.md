---
title: "The Expert-in-the-Loop Illusion: AI for Me vs. AI for Everyone"
date: 2026-04-25
description: "There's a massive gap between using AI agents as a domain expert who can course-correct, and building agents that work for everyone. Most teams underestimate this gap."
tags: ["agentic-ai", "context-engineering", "ai-safety"]
author: "Steven Leung"
draft: false
---

With the breakthrough models and agent harnesses that have shipped over the past six months or so, everyone is feeling the power of having an agent coworker. I still remember the first time using Claude Code with Opus 4.5 and spinning up an app for my wife's PR business in just a couple of hours. I'm not a frontend engineer. I've never been a frontend engineer. But suddenly I was watching a real application render (backend, frontend, the whole thing) while I focused on the actual business problems we were trying to solve instead of how to write the code. The experience was shocking, perspective-changing, and intoxicating.

Since then, my core work has never been the same. Coding agents are integral to everything I do: not just writing code, but documentation, planning, brainstorming. Basically every task starts with invoking Claude or Codex. These agents genuinely feel like extremely competent coworkers, running autonomously on complex tasks that would take me hours, often without needing additional feedback from me.

And that's where the trap is.

## The natural next question

Similar to the moment of awe we've all had using these coding agents, I think most of us have also had the moment of wondering: what tasks and workflows can I just put an agent out there as a self-sufficient, user-facing system?

It seems extremely possible. The agent is already doing the work. I'm barely intervening. Why not package this up and let other people use it?

Before I go further, let me be specific about what I mean by a "user-facing agent," because it's a different thing than what most of us use day-to-day. When I talk about an interactive agent, I mean the way most of us work with Claude Code or similar tools: you're in a session, you're prompting, you're watching the output, you're course-correcting in real time. You are in the loop.

A user-facing agent is something different. It's a system you've built on top of an LLM and agent harness that other people interact with. People who don't have your context, your domain expertise, or your ability to spot when the agent is wrong. Think of a customer support agent, a data analyst assistant, an operations copilot. The agent has been given persistent context, structured tools, and a defined scope, and it's expected to operate reliably without you watching over its shoulder.

The gap between these two things is enormous. And I didn't fully appreciate how enormous until I tried to cross it.

## What happened when I tried

After building the PR business app, I wanted to add a user-facing finance agent. The idea was straightforward: the agent would sit on top of all the business financial data and be able to answer any finance question (who owes us money, what's our revenue this quarter, which clients are overdue) and also take actions like sending invoices.

I had been working with this data interactively for weeks. I knew the clients, the data model, the quirks. When I asked the agent financial questions in my own sessions, it was great. So I wired it up as a user-facing system with persistent context, tools for querying data and sending invoices, and pointed it at the same data.

On the first question, it broke down. It got confused about who the clients were. It was far less aware of the business workings and the nuances of the data than I expected. It felt like a completely different system than the one I'd been working with interactively.

When I dug into why, I found something revealing. Over the course of building the app, we had evolved through two different data models. The agent's persistent memory hadn't been fully updated to reflect the current model, and some of that stale memory had been used to seed the user-facing agent's context. In my interactive sessions, I would have caught this immediately. I would have seen the agent reference the wrong client structure and corrected it. But in the user-facing system, there was no one to catch it. The stale context just silently produced wrong answers.

## The illusion

I saw similar patterns when building a data analyst agent and an operations assistant in other settings. The details were different, but the shape of the failure was the same: systems that worked well with me in the loop fell apart without me.

This experience crystallized something I'd been sensing but hadn't articulated. When I described the interactive agent as running "autonomously without needing additional feedback from me," that wasn't quite true. I *was* providing feedback. Constantly, implicitly, without even registering it.

Every time I scanned the output and moved on, that was implicit validation. Every time I noticed something slightly off and rephrased my prompt, that was course correction. Every time I chose to use one tool over another based on what I knew about the data, that was domain expertise flowing into the system. I was the guardrail the entire time. I just didn't notice because it felt effortless.

This is the expert-in-the-loop illusion. The combined system (me plus the agent) is highly capable. But the agent alone, stripped of my continuous implicit oversight, is not the same system. And the delta between those two is where user-facing agents fall apart.

## The specific challenges

Across these projects, I've identified the specific ways the gap manifests:

**1. You're building more nuanced context than you realize.**

In an interactive session, every prompt you write, every follow-up question, every correction is adding context that the agent uses to do better work. You're essentially training the agent on your domain in real time, across the conversation.

When you try to translate that into persistent context for a user-facing system (system prompts, memory stores, tool descriptions) you have to make that implicit context explicit. And you'll miss things. The finance agent example is a case in point: I didn't realize that our data model had evolved in a way that created contradictions in the agent's memory, because in my interactive sessions I was resolving those contradictions unconsciously.

**2. Autonomy and guardrails trade off differently.**

In interactive sessions, it's easy to give the agent maximum autonomy (full bash access, broad tool usage) because I'm in the loop to approve or deny actions and course-correct if things go sideways. I can let the agent try risky things because I'll catch the bad ones.

In user-facing environments, you want tools to be more limited and least-privileged to avoid disasters. But this limitation degrades results. The agent that was brilliant with full autonomy under my supervision becomes clumsy with restricted tools and no expert to guide it. Combine this with the context problem above, and you get a system that's both less informed and less capable than the one you tested with.

**3. The stakes are quietly higher.**

In an interactive session, a wrong answer is cheap. I see it, I correct it, we move on. The feedback loop is tight and the cost of a mistake is a few seconds of my time.

In a user-facing system, a wrong answer gets accepted. The user isn't a domain expert. They asked the agent a question precisely because they don't know the answer themselves. When the agent confidently returns something plausible but wrong, the user has no basis to question it. They act on it.

This is the part that I think gets underappreciated. It's not just that user-facing agents perform worse (challenges 1 and 2). It's that the consequences of that worse performance are amplified because there's no expert in the loop to catch and correct the errors. In my interactive sessions, the agent made mistakes constantly. I just didn't think of them as mistakes because I caught and fixed them so naturally. In a user-facing system, those same mistakes become the final output.

## What I'd recommend

After working through these problems across multiple projects, I've landed on a few patterns that help close the gap. I want to be honest that none of them fully solve it, but they've meaningfully reduced the distance between what works in my interactive sessions and what holds up for end users.

**Mirror your interactive and user-facing tool usage.**

When building a user-facing agent, try to use the same tools in your own interactive sessions. This might feel limiting at first, since your interactive agent probably started with general-purpose tools. But once you've designed the user-facing toolset, switch to it yourself. When you hit friction in your own workflow, you're finding the same friction your users will hit. Every time you see the interactive agent call a tool wrong or produce a bad result with the constrained toolset, that's a bug you can fix before users see it.

**Build agent tools as close to your application logic as possible.**

When user-facing agents wrap around an application, design the agent's tools to sit on top of the application's existing APIs and business logic, not alongside them. The application has already thought through what operations make sense, what validations are needed, what sequences of actions are valid. Tools that reuse that logic give the agent the best chance of doing the right thing. Tools that bypass it and hit the data layer directly are where things go wrong.

**Don't skip evaluation because you're in the agentic era.**

I feel like the discipline of systematic evaluation got lost in the transition from chatbots to agents. When everyone is shipping agentic features fast, building a proper eval system feels like it's slowing you down. But for user-facing agents, it's essential:

- Build test sets that cover the realistic range of user queries
- Create an evaluation framework that measures correctness, not just completion
- Measure performance over time to catch drift as data and context evolve
- Run stratified analysis across different query types and user scenarios

This matters even more for user-facing agents than it did for chatbots, because the failure modes are subtler. The agent doesn't crash. It confidently gives wrong answers.

## Where this leaves us

I don't think this is a reason to stop building user-facing agents. But I think the industry is underestimating the gap between "this works great when I use it" and "this works great when anyone uses it." The former is a tool. The latter is a product. And the distance between them is not primarily an engineering problem. It's a knowledge transfer problem. How do you encode the domain expertise that made the expert-in-the-loop version work into a system that doesn't have that expert?

This question becomes even more pointed when you consider where the industry is heading. The current trajectory isn't just toward better copilots or smarter assistants. It's toward fully autonomous agent workers: systems that can take on entire job functions, operate independently across complex domains, and make consequential decisions without human review. That's the vision driving massive investment right now.

But if we're still struggling to make a finance agent reliably answer questions about a small business's clients (a scoped, well-defined problem with structured data), what does that tell us about deploying autonomous agents to manage entire business functions? The challenges I've described here don't get easier at that scale. They get harder. The context becomes richer, the edge cases multiply, and the cost of undetected errors grows.

I'm not saying autonomous agent workers are impossible. I'm saying that the path from here to there runs directly through the expert-in-the-loop problem. Until we get meaningfully better at encoding domain expertise into systems that can operate without that expert, the gap between what agents can do *with us* and what they can do *for others* will remain the bottleneck.

That's the hard problem. And I think it's one of the most important problems in agentic AI right now, because it sits at the intersection of capability, reliability, and safety. An agent that works brilliantly for an expert and fails silently for everyone else isn't just a product problem. It's a trust and safety problem.

I'm continuing to work on this across the systems I'm building. I'd be curious to hear if others are hitting the same wall.
