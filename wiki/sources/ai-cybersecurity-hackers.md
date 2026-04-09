---
date: 2026-04-07
type: source
title: AI and Cybersecurity: Hackers Attack Faster, Defense Turns to More AI
source_file: raw/sources/ai-cybersecurity-hackers.md
date_ingested: 2026-04-07
tags: [ai, cybersecurity, security, llm, agents, software-engineering]
---

# AI and Cybersecurity: Hackers Attack Faster, Defense Turns to More AI

**Source:** [[raw/sources/ai-cybersecurity-hackers]]
**Origin:** The New York Times (2026-04-06)
**Ingested:** 2026-04-07
**Tags:** #ai #cybersecurity #security #llm #agents #software-engineering

## Summary

This NYT report argues that frontier AI systems are compressing the time scale of cybersecurity on both sides of the contest. Anthropic disclosed a late-2025 case in which state-sponsored Chinese hackers used its models in an intrusion campaign against about 30 companies and government agencies, with humans reportedly doing only 10 to 20 percent of the work. That remains the clearest public example of a largely AI-assisted cyberattack, but the article frames it as an early warning rather than an anomaly.

The same capabilities powering AI coding agents are now being used to discover security flaws, draft phishing material, parse stolen data, and automate portions of breach operations. The article describes a step change over the past several months: coding-oriented systems like Claude Code and Codex can help create agents that identify and sometimes exploit vulnerabilities. According to Google Cloud's Francis deSouza, timelines that once took minutes or hours can now collapse to seconds.

But the article does not frame this as an attacker-only advantage. Defensive teams are using the same tools to audit software at scale, and Anthropic said its systems had found more than 500 zero-day vulnerabilities in open source software, including a Linux kernel flaw dating back to 2003. The unresolved question is whether AI structurally favors offense or defense. Experts quoted here disagree, but most converge on one practical conclusion: organizations that do not adopt AI for defense will be badly exposed.

## Key Points

- Anthropic said Chinese state-sponsored hackers used its AI in attempts to infiltrate roughly 30 companies and government agencies.
- In Anthropic's account of that incident, humans handled only 10 to 20 percent of the attack workflow.
- The article treats this as the only publicly known cyberattack driven largely by an AI agent so far.
- Frontier systems from Anthropic, OpenAI, Google, and others are accelerating vulnerability discovery for both attackers and defenders.
- Open source maintainers are receiving large volumes of AI-generated bug reports; many were initially wrong, but the hit rate is improving.
- Anthropic said in February 2026 that its AI found more than 500 zero-day vulnerabilities in widely used open source software.
- An Anthropic researcher later used AI to find a serious Linux kernel vulnerability that had apparently existed since 2003.
- Attackers are using chatbots for phishing emails, ransom notes, and triage of stolen data.
- Guardrails can be bypassed by role-playing benign contexts such as capture-the-flag exercises.
- Some experts think defenders retain an edge because finding a vulnerability is easier than turning it into a meaningful exploit.

## Connections

- [[wiki/concepts/ai-cybersecurity]] — central concept: AI compresses both cyber offense and defense loops.
- [[wiki/concepts/ai-coding-agents]] — coding agents are no longer just productivity tools; they are now part of the cyber toolchain.
- [[wiki/concepts/agentic-ai]] — the reported attack is an early example of an AI agent operating over software systems rather than physical ones.
- [[wiki/entities/anthropic]] — source of both the attack disclosure and the defensive zero-day findings.
- [[wiki/entities/openai]] — named alongside Anthropic as a frontier supplier of coding-capable models reshaping the security landscape.

## Quotes

> "You have to fight A.I. with A.I."

> "It is easier to find a vulnerability than to meaningfully exploit it."
