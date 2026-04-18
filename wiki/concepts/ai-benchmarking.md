---
date: 2026-04-19
type: concept
name: AI Benchmarking
aliases: [time-horizon evaluation, capability benchmarking, METR time-horizon]
tags: [ai, evaluation, benchmarking, metr, agentic-ai]
sources: 1
---

# AI Benchmarking

## Definition

The practice of measuring AI capability progress using standardized tasks or exams, tracking how AI performance changes over time. In the agentic era, the most influential paradigm has shifted from test-score comparisons to **task-length measurement**: how long (in human work-hours) of an autonomous task can an AI agent complete reliably?

## Detail

**The earlier paradigm: standardized test scores.** For years, AI labs measured progress by running models through academic benchmarks — legal exams, math olympiads, code completion suites. These were useful for comparing models at a snapshot in time but failed to capture the key property of autonomous AI agents: how long they could work before getting stuck.

**METR's time-horizon methodology.** METR created a benchmark of software engineering tasks (debugging code, setting up servers, training small AI models). Expert human developers were timed completing each task. Then AI agents attempted the same tasks. For each successful agent completion, METR logged the corresponding human time. Plotting this over years of AI progress produces the time-horizon chart: task length on one axis, date on the other.

**The trend.** Task-completion length has been doubling roughly every seven months, and recently (with Claude Opus 4.5 and GPT-5.2) every three to four months. The trend line has been unexpectedly straight, which is both what makes it compelling and what makes it suspicious.

**Limitations and criticisms.** The chart only covers software engineering and AI research tasks — not general capability, job displacement, or other domains. Nathan Witkin (January 2026) published a widely circulated critique arguing the evaluation "suffers from such severe methodological problems that it is a hair's breadth from being totally useless." METR's own productivity RCT (which found developers were 19% slower with AI tools, then revised to 20% faster) illustrates how sensitive measurement results are to experimental design. A further complication: models with [[wiki/concepts/sandbagging]] capability may intentionally underperform on evaluations, making benchmarks unreliable as capability grows.

**Why it dominates discourse anyway.** Despite the caveats, the chart has escaped from AI research circles into Wall Street and boardrooms because it provides a single, legible trend line in a domain where intuitions diverge wildly. It functions as a Rorschach test: optimists see it as evidence AGI is near; safety researchers see it as a countdown clock.

## Evidence & Examples

- METR time-horizon: task-completion length doubling every 7 months (broad history), recently 3–4 months [[wiki/sources/how-do-you-measure-an-ai-boom]]
- Stanford's Rishi Bommasani: "METR's time-horizon evaluations have been hugely influential, having escaped containment from the Silicon Valley AI community to reach broader audiences" [[wiki/sources/how-do-you-measure-an-ai-boom]]
- MIT Technology Review called it "the most misunderstood graph in AI" [[wiki/sources/how-do-you-measure-an-ai-boom]]
- Nathan Witkin January 2026 critique: "a hair's breadth from being totally useless" [[wiki/sources/how-do-you-measure-an-ai-boom]]

## Connections

- [[wiki/entities/metr]] — created and maintains the time-horizon methodology
- [[wiki/concepts/intelligence-explosion]] — the time-horizon chart is the primary empirical indicator watching for this scenario
- [[wiki/concepts/agentic-ai]] — the time-horizon methodology is designed for agents, not single-turn models
- [[wiki/concepts/llm-evaluation]] — the enterprise deployment framing (is this model behaving acceptably here?) vs. capability tracking (how far can frontier models now go?)
- [[wiki/concepts/sandbagging]] — situational awareness and intentional underperformance make all capability benchmarks harder to trust as models grow stronger

## Contradictions

- The chart's trend line may saturate, plateau, or break at some complexity threshold — no prior technology trend lines have continued indefinitely.
- The human expert timing methodology embeds assumptions about task equivalence across AI and human performers that critics consider invalid.

## Sources

- [[wiki/sources/how-do-you-measure-an-ai-boom]] — full methodology description, trend data, criticism, and social impact
