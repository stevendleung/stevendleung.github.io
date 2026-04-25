---
title: "AI Can Write the Code. It Can't Understand Your Data."
date: 2026-04-25
description: "Agentic coding tools excel at software implementation but hit a wall when the real challenge is understanding complicated, inter-relational data."
tags: ["agentic-ai", "context-engineering", "ml-engineering"]
author: "Steven Leung"
draft: true
---

AI coding agents are remarkably good at building software. Give them a clear spec and they'll scaffold an app, write an API, refactor a module, set up tests. The implementation layer of software development has gotten dramatically easier.

But there's a category of work where these tools fall apart, and it's one that I hit constantly: when the hard part isn't writing code, but understanding what the data actually means.

## Where the tools excel

Let me be specific about what works well, because I don't want this to read as a complaint. I use AI coding agents daily and they've transformed how I work. They're excellent at:

- Implementing well-defined functions and classes
- Scaffolding applications and APIs from a description
- Refactoring existing code to new patterns
- Writing tests for code that already exists
- Navigating and explaining unfamiliar codebases

In all of these cases, the structure and intent are relatively clear. The agent knows what "correct" looks like because correctness is defined by syntax, type systems, test assertions, or explicit specifications.

## Where they break down

The problems start when the real challenge is making sense of data that's messy, nuanced, and inter-relational. The kind of data where:

- Field names don't tell the full story. What does `status = 3` mean? It depends on which system wrote it, when, and what other fields accompany it.
- Relationships between entities are implicit. Two tables are related, but not through a foreign key. The relationship is a business rule that lives in someone's head.
- Edge cases carry domain-specific meaning. A null value in one context means "not applicable" and in another means "unknown" and in a third means "something went wrong."
- The same data means different things at different points in time. A record that looked one way when it was created means something entirely different after three status transitions.

<!--
TODO: Add a concrete example from your work. Something like:
"At Duo, I worked with [anonymized description of a messy data challenge]. The data had [specific complexity]. When I tried to use an AI coding agent to help build the analysis pipeline, it produced code that looked correct, ran without errors, and produced plausible-looking results that were wrong because it didn't understand [specific nuance]."
-->

## The false confidence problem

This is the most dangerous part. When an AI agent misunderstands your data model, it doesn't crash. It doesn't throw an error. It writes code that runs, produces output, and looks reasonable.

But the output is subtly wrong because the agent made an assumption about what the data means, and that assumption was plausible but incorrect. If you're the domain expert, you catch it. If you're not, you ship it.

<!--
TODO: Another concrete example would strengthen this section.
-->

## The bottleneck has shifted

What I've come to realize is that for a large class of real-world problems, the bottleneck in software development was never the code. It was understanding the data well enough to know what code to write.

AI coding agents have removed the implementation bottleneck. That's genuinely valuable. But they've exposed the data comprehension bottleneck that was always there, hidden behind the effort of writing the code.

The human still has to do the hard cognitive work of making sense of the data: understanding the relationships, the edge cases, the domain-specific semantics. Once that understanding exists, the agent can implement it rapidly. But the understanding itself is the hard part, and it's the part the agent can't reliably do.

## What this means going forward

I don't think this is a permanent limitation. Better context engineering, longer context windows, and domain-specific fine-tuning will all help. But right now, anyone using AI coding tools on data-intensive problems should know where the boundary is.

The agent is a fast, capable implementer. It is not yet a thinking partner on data semantics. Knowing the difference will save you from shipping confident-looking code that's quietly wrong.
