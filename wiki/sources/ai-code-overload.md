---
type: source
title: AI Code Overload — The Glut Nobody Planned For
source_file: raw/sources/ai-code-overload.md
date_ingested: 2026-04-07
tags: [ai-coding, software-engineering, security, llm, agents, productivity]
---

# AI Code Overload — The Glut Nobody Planned For

**Source:** [[raw/sources/ai-code-overload]]
**Origin:** The New York Times (2026)
**Ingested:** 2026-04-07
**Tags:** #ai-coding #software-engineering #security #llm #agents #productivity

## Summary

A NYT investigation into the unintended consequences of AI coding tools going mainstream. The central finding: AI coding agents (Claude Code, Codex, Cursor) have upgraded from "occasionally helpful" to "full-fledged code-generating wizards" — and the result is a code production glut that organizations cannot review, secure, or manage at the same pace.

One financial services company went from 25,000 to 250,000 lines of code/month after adopting Cursor — creating a backlog of 1 million lines needing review. The bottleneck has shifted entirely from *writing* code to *reviewing and securing* it. There aren't enough application security engineers to fill the gap, and the problem is cascading: faster code → faster demands on sales, marketing, support; AI-generated open source contributions overwhelming maintainers; engineers downloading entire codebases to laptops for AI tool compatibility, creating novel security risks.

The ironic proposed solution: more AI (code-reviewing agents) to handle the code that AI coding agents produced.

## Key Points

- Company case: 25K → 250K lines/month post-Cursor → 1M line review backlog. [[Joni Klippert, StackHawk]]
- 90% of software developers now use AI to help work; 71% of coders use AI (Google/DORA 2025 survey).
- AI coding agents leveled up in November 2025 (Anthropic Claude Code + OpenAI Codex releases) — described as transformative, not incremental.
- "Projects that once required hundreds of engineers can now be done by tens." — Andrew Bosworth, Meta CTO.
- **New bottleneck**: not enough application security engineers — "not enough on the planet to satisfy what just American companies need."
- Novel security risk: AI tools work better locally than in secure cloud environments → engineers downloading entire codebases to laptops.
- Open source projects flooded with AI-generated contributions; tldraw closed external contributions entirely in January 2026.
- Accountability gap: unclear whose responsibility AI-generated code bugs are.
- "The software development factory kind of broke." — Tido Carriero, Cursor head of engineering.
- Counter-movement: Elvex rule — all code must be reviewed by a human, or "no one will understand why it broke."
- Cursor acquired Graphite (code-reviewing bots) in December 2025; AI reviewing AI code is the emerging answer.

## Connections

- [[wiki/concepts/ai-coding-agents]] — the central subject; Claude Code, Codex, Cursor as the agents causing the shift.
- [[wiki/concepts/agentic-ai]] — AI coding agents are a direct consumer instance of agentic AI; same architecture, applied to software development.
- [[wiki/concepts/deep-work]] — **key contradiction**: AI tools dramatically increase code *volume*, but the human review work created is cognitively demanding deep work. More AI output → more human deep work required, not less.
- [[wiki/entities/anthropic]] — Claude Code cited as a key agent that "leveled up" in November 2025.
- [[wiki/entities/cursor]] — primary AI coding tool in the article; acquired Graphite for code review.

## Quotes

> "The sheer amount of code being delivered, and the increase in vulnerabilities, is something they can't keep up with." — Joni Klippert, StackHawk CEO

> "The blessing and the curse is that now everyone inside your company becomes a coder." — Michele Catasta, Replit

> "There are not enough application security engineers on the planet to satisfy what just American companies need." — Joe Sullivan, Costanoa Ventures

> "The software development factory kind of broke." — Tido Carriero, Cursor

> "It's just going to break something, and they're not going to know why it broke." — Sachin Kamdar, Elvex
