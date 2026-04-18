---
date: 2026-04-07
type: concept
name: Agentic AI
aliases: [AI agents, autonomous agents, agentic systems]
tags: [ai, agents, robotics, manufacturing, llm]
sources: 5
---

# Agentic AI

## Definition

AI systems that **reason, plan, and act** autonomously on large-scale processes — going beyond single-turn question answering to execute multi-step tasks, respond to changing conditions, and operate within broader systems with minimal human supervision.

## In Manufacturing / Smart Factories

In industrial contexts, agentic AI encompasses both physical and digital automation [[wiki/sources/robotics-trends-2026]]:
- Managing supply chain disruptions in real time
- Optimizing production flow and uptime
- Coordinating customer experience and order fulfillment
- Physical robots executing tasks within these pipelines

The key distinction from earlier automation: agentic systems *reason* about their context rather than following fixed rules. A rule-based system handles the expected case; an agentic system adapts when conditions change.

## In Cybersecurity

Cybersecurity is another domain where agentic AI now operates over large, messy environments. Instead of moving robots or coordinating supply chains, the agent works over codebases, services, credentials, and software tools: finding weaknesses, chaining actions, and gathering sensitive information with limited human supervision.

The Anthropic-reported intrusion campaign described in [[wiki/sources/ai-cybersecurity-hackers]] is important because it is an early public example of this pattern. In Anthropic's telling, human operators handled only 10 to 20 percent of the workflow, making the cyberattack meaningfully agentic rather than just AI-assisted at the margins.

## Relation to Schema-Driven Agents

This wiki is itself an example of agentic AI: Claude reads context, follows a schema (CLAUDE.md), reasons about which pages to update, plans the sequence of writes, and executes — all without turn-by-turn human instruction. The difference between this wiki agent and a factory agentic AI is the output medium (markdown files vs. physical processes), not the underlying architecture. [[wiki/concepts/schema-driven-agents]]

## Relation to Physical AI

Agentic AI is the *cognitive layer*; Physical AI is the *embodied layer*. In a smart factory:
- Agentic AI plans and coordinates (supply chain, scheduling, quality decisions)
- Physical AI executes (robots responding to the plan with sensorimotor action)

Together they form the complete autonomous factory stack. [[wiki/concepts/physical-ai]]

## In IoT Actor Networks

IIoT actor nodes are a concrete, deployed form of agentic AI. A warehouse where AI robots negotiate task allocation and resolve routing conflicts in real time is a multi-agent agentic system operating in the physical world. The LLM layer enables structured communication between agents — expressing intentions and constraints — while each node acts autonomously within those bounds. [[wiki/concepts/industrial-iot]]

The same pattern at different scales: this wiki agent (markdown files) → AI coding agents (codebases) → IIoT actor nodes (physical processes) → warehouse robot fleets (multi-agent physical systems). Each is agentic AI; the output medium and stakes differ.

## In the Workplace

Agentic AI is now penetrating organizational management: tools that automate scheduling, synthesize performance reviews, monitor project timelines, and surface early warning signals about team dysfunction are being deployed to support managers overseeing significantly more people than before. This is both the cause and the justification for the **megamanager era** — span-of-control inflation from ~6 to ~12 direct reports on average.

The key open question (from [[wiki/concepts/expertise-paradox]]): are these tools automating the administrative scaffolding of management, freeing managers to do more coaching and strategic work? Or are they enabling span-of-control levels that make even the expert parts of management impossible? [[wiki/sources/megamanager-era-how-many-direct-reports-ai-middle-management]]

## Connections

- [[wiki/concepts/ai-cybersecurity]] — cybersecurity is now a major digital operating environment for agentic systems.
- [[wiki/concepts/physical-ai]] — agentic AI's physical embodiment in robotics.
- [[wiki/concepts/ai-coding-agents]] — the most widely deployed consumer instance of agentic AI; AI coding tools like Claude Code and Cursor.
- [[wiki/concepts/schema-driven-agents]] — the same agent architecture: schema defines context + rules; LLM reasons and acts. Smart factories use the same paradigm at industrial scale.
- [[wiki/concepts/robotics-multidisciplinarity]] — agentic AI is raising the importance of CS/AI entry paths into robotics.
- [[wiki/concepts/industrial-iot]] — IIoT actor nodes and warehouse robot fleets are agentic AI in deployed physical systems.
- [[wiki/concepts/expertise-paradox]] — whether workplace agentic AI augments or hollows managers depends on which tasks it automates.
- [[wiki/concepts/span-of-control]] — agentic AI is the enabling technology behind span-of-control inflation.

## The Time-Horizon Measure of Agentic Progress

The most influential empirical measure of agentic AI capability is METR's time-horizon chart: it tracks the length (in human expert hours) of software engineering task an AI agent can complete *reliably*. The task length has been doubling roughly every seven months since METR began tracking it, and recently (with Claude Opus 4.5 and GPT-5.2) the doubling has accelerated to every three to four months. This is effectively a clock measuring how autonomous AI agents are becoming. If the trend continues, it implies that agents could eventually handle the entire R&D cycle for training a new frontier model — the precondition for [[wiki/concepts/intelligence-explosion]]. [[wiki/sources/how-do-you-measure-an-ai-boom]]

## Sources

- [[wiki/sources/robotics-trends-2026]] — identifies agentic AI as a key 2026 smart factory trend.
- [[wiki/sources/ai-code-overload]] — AI coding agents as the most widely deployed real-world agentic AI application.
- [[wiki/sources/the-intelligent-edge-how-ai-and-large]] — multi-agent actor node coordination in warehouses; LLM-mediated robot negotiation.
- [[wiki/sources/ai-cybersecurity-hackers]] — early public example of agentic AI being used in a largely AI-driven cyberattack.
- [[wiki/sources/megamanager-era-how-many-direct-reports-ai-middle-management]] — agentic AI automating workplace coordination as driver of the megamanager era.
- [[wiki/sources/how-do-you-measure-an-ai-boom]] — METR time-horizon chart as the primary empirical measure of agentic capability progress; doubling trend data.
