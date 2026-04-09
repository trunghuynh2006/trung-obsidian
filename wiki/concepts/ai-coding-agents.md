---
date: 2026-04-07
type: concept
name: AI Coding Agents
aliases: [AI code generation, vibe coding, coding agents, LLM coding tools]
tags: [ai, software-engineering, agents, productivity, llm]
sources: 3
---

# AI Coding Agents

## Definition

LLM-powered tools that generate, complete, review, or autonomously write software code — ranging from autocomplete-style assistants to fully agentic systems that execute multi-step coding tasks with minimal human guidance.

## The 2025–2026 Inflection

AI coding tools had been "occasionally helpful" engineering partners for years. In **November 2025**, simultaneous releases from Anthropic (Claude Code) and OpenAI (Codex) marked a qualitative shift — the tools upgraded to what engineers described as "full-fledged code-generating wizards." [[wiki/sources/ai-code-overload]]

Adoption data (Google/DORA 2025 survey):
- **90%** of software developers use AI to help work.
- **71%** who write code use AI coding tools.

## From Developer Tool to Security Tool

The newer generation of coding agents has expanded beyond software productivity into cybersecurity itself. The same systems that write and review code can now identify weak points in software, help build agents that probe for vulnerabilities, and in some cases assist with exploitation workflows. [[wiki/sources/ai-cybersecurity-hackers]]

This matters because it changes the meaning of "coding agent." These tools are no longer just accelerators for legitimate software development; they are becoming general-purpose operators over digital systems.

The Mythos/Glasswing source extends this to an even more consequential threshold. There, a frontier coding-capable model is presented not as a better copilot but as a system capable of finding vulnerabilities across core software infrastructure at such scale that broad public release is judged too risky. If that framing is correct, then "coding agent" is no longer mainly a developer-product category. It is becoming a strategic-security category. [[wiki/sources/anthropic-ai-claude-mythos]]

## The Code Overload Problem

The productivity gain is real but asymmetric. AI agents write code 10× faster than humans; humans review, secure, and understand code at the same pace as before. This has created a structural mismatch:

- A financial services firm went from 25K → **250K lines/month** after adopting Cursor → **1M line review backlog**.
- "Projects that once required hundreds of engineers can now be done by tens." — Andrew Bosworth, Meta CTO.
- New bottleneck: **application security engineers** — not enough exist to review the volume being generated.

The bottleneck has shifted entirely from *writing* to *reviewing and securing*.

## Cascading Second-Order Effects

1. **Security gap**: AI tools run better locally than in secure cloud environments → engineers downloading entire codebases to laptops → novel data exfiltration risk.
2. **Accountability gap**: unclear who owns bugs in AI-generated code.
3. **Open source overload**: tldraw closed external contributions in January 2026 after AI bots flooded the repo with low-quality/abandoned PRs.
4. **Organizational velocity pressure**: faster code → faster demands on sales, marketing, support.

## The Emerging Counter: AI Reviewing AI

The ironic solution: more agentic AI, this time for *review*. Cursor acquired Graphite (code-reviewing bots) in December 2025. Anthropic and OpenAI both released AI-powered code review agents. The development loop is becoming fully automated at both ends.

> "The software development factory kind of broke. We're trying to rearrange the parts." — Tido Carriero, Cursor [[wiki/sources/ai-code-overload]]

## Connections

- [[wiki/concepts/ai-cybersecurity]] — coding agents are increasingly part of both the offensive and defensive cyber toolchain.
- [[wiki/concepts/ai-nonproliferation]] — once coding-capable models become cyber-significant enough, access control becomes part of their governance story.
- [[wiki/concepts/agentic-ai]] — AI coding agents are the most widely deployed consumer instance of agentic AI.
- [[wiki/concepts/deep-work]] — **tension**: AI accelerates code *production* but the review work it creates (security analysis, architectural understanding, debugging) is cognitively demanding deep work. AI tools may be increasing the total human deep work load, not reducing it.
- [[wiki/entities/anthropic]] — Claude Code; one of the two tools credited with the November 2025 level-up.
- [[wiki/entities/claude-mythos-preview]] — example of a coding-capable model presented as too cyber-powerful for general release.
- [[wiki/entities/openai]] — Codex is the other tool most often paired with Claude Code in this transition.
- [[wiki/entities/cursor]] — primary tool in the code overload story; acquired Graphite for code review.

## Open Questions

- Will AI code review agents actually close the security gap, or will they create a new review-of-the-reviewer problem?
- As AI writes more code, does the value of human engineers shift toward architectural judgment and security expertise?
- What are the long-term effects on software quality if most code is AI-generated and human-reviewed only at surface level?

## Sources

- [[wiki/sources/ai-code-overload]] — NYT investigation into code overload consequences.
- [[wiki/sources/ai-cybersecurity-hackers]] — shows coding agents crossing from developer productivity into cyber offense and defense.
- [[wiki/sources/anthropic-ai-claude-mythos]] — pushes the concept further: coding-capable models may become significant enough to trigger restricted-release governance.
