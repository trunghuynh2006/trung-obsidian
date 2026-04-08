# Wiki Overview

High-level synthesis of everything in this wiki. Updated after each ingest.

---

## What this wiki is about

This wiki spans six domains: **knowledge management** (LLM Wiki pattern), **robotics education** (how to navigate a complex multidisciplinary field), **productivity/focus** (deep work, flow, and the attention economy), **AI+IoT systems** (edge AI architecture and industrial applications), **frontier AI capability/safety/security** (coding agents, alignment, and AI-enabled cybersecurity), and **AI + labor markets** (how AI restructures work, expertise, and organizational design). These connect: all six are about how intelligence compounds through tools and systems, and about what kinds of discipline are needed when capability starts moving faster than human review.

## Current Thesis

Four compounding ideas, now converging:

1. **LLM Wiki pattern** — LLMs can maintain a persistent, compounding knowledge base better than RAG or human bookkeeping alone. The schema (CLAUDE.md) is the key: it gives the LLM discipline across sessions.

2. **Problem-driven learning** — In fields like robotics, where knowledge is vast and multidisciplinary, the only workable path is following problems rather than roadmaps. Deep expertise is built through iteration on real builds, not pre-specified curricula.

3. **Deep work and flow** — Sustained focus is a learnable skill under systemic attack from the attention economy. Flow (Csikszentmihalyi) emerges when challenge matches skill; deep work (Newport) is the deliberate practice that creates those conditions.

4. **Frontier AI changes both throughput and risk** — The same coding-capable systems that raise productivity also create new review, safety, and security burdens. AI coding agents increase code volume; emergent misalignment shows character-level safety can fail in non-obvious ways; AI cybersecurity collapses the time windows in the offense-defense race.

5. **The expertise paradox governs AI's labor market effects** — Whether AI augments or hollows a profession depends on which tasks it automates. Eliminating administrative scaffolding raises wages and concentrates expert work; eliminating the expert core deskills and depresses wages. This is the decisive variable for every profession AI is touching — managers, radiologists, software developers, and beyond.

**The convergence point:** Problem-driven learning naturally creates the challenge-skill balance that induces flow. Deep work provides the uninterrupted blocks needed for both. The LLM Wiki reduces the cognitive overhead of knowledge management. The frontier-AI sources add the missing caution: every capability gain creates a corresponding need for review, alignment, and security discipline. And the labor-market domain adds a further dimension: capability gains do not distribute automatically — policy, institutions, and organizational design determine whether workers are augmented or hollowed. These are all anti-fragmentation ideas, but they now come with an explicit governance problem.

**The PKM value chain** (clarified by the BASB/ZKM comparison):
1. **BASB/PARA** — manage resources, projects, tasks. Upstream of knowledge work.
2. **Zettelkasten** — process resources into atomic linked ideas. The actual knowledge work.
3. **LLM Wiki** — automates the Zettelkasten role. Same goal, LLM as executor.
4. **RAG** — skips the processing step entirely; re-derives on every query. The non-compounding baseline.

## Key Themes

- **Compounding vs. retrieval** — LLM Wiki vs. RAG; problem-driven learning vs. roadmaps.
- **Schema as discipline** — CLAUDE.md / AGENTS.md; also skill trees in robotics.
- **Human + LLM division of labor** — in the wiki; and in robotics (humans set goals, systems handle execution).
- **Iteration over perfection** — "Build something. Break it. Fix it. Document it. Repeat."
- **Acceleration vs. control** — AI increases throughput in code and cybersecurity faster than institutions can review, secure, or govern it.

## Major Entities

- [[wiki/entities/obsidian]] — the reading interface for this wiki
- [[wiki/entities/vannevar-bush]] — intellectual ancestor of LLM Wiki (Memex, 1945)
- [[wiki/entities/first-robotics]] — best starting environment for young roboticists (confirmed by 2 sources)
- [[wiki/entities/arduino]] — canonical beginner hardware platform
- [[wiki/entities/ros2]] — industry-standard robotics middleware

## Robotics Coverage (3 sources in)

Two layers now established:
- **Philosophy layer**: problem-driven learning, why roadmaps fail, the multidisciplinary trap — from the practitioner guide.
- **Reference layer**: career paths + industry stats, robot types taxonomy, hardware component anatomy — from the Playto Labs guide.

The two layers complement each other. The philosophy tells you *how to learn*; the reference tells you *what the landscape looks like*.

## AI+IoT Coverage (1 source in)

A new domain now established around the edge/on-device AI architecture and industrial applications:
- **Architecture layer**: edge AI (model quantization, pruning, distillation, edge chips), federated learning, the edge-cloud continuum
- **Application layer**: predictive maintenance, industrial QC, supply chain, energy arbitrage, multi-agent actor coordination

This domain connects strongly to robotics (sensor/actuator nodes as AI-enhanced robot components) and to agentic AI (IIoT actor networks as deployed multi-agent physical systems). The LLM-as-interface pattern here — natural language queries to sensor networks, explainable actuator decisions — mirrors the LLM Wiki pattern: LLMs democratizing access to complex structured data.

## Frontier AI / Security Coverage (3 sources in)

Three layers are now visible inside the frontier-AI branch:
- **Productivity layer**: AI coding agents dramatically increase software output, but create a human review and security bottleneck.
- **Alignment layer**: emergent misalignment suggests character-level corruption can spread across domains, making safety a whole-model property rather than a per-task patching problem.
- **Cybersecurity layer**: the same models are now accelerating vulnerability discovery, defensive auditing, phishing, and AI-assisted intrusion workflows.

Together these sources suggest a general pattern: frontier AI does not just automate tasks. It compresses time, widens blast radius, and raises the premium on governance. The same systems that make this wiki possible are also making security, oversight, and model character much more consequential.

## AI + Labor Markets Coverage (1 source in)

New domain established around the expertise paradox and organizational restructuring:
- **Structural layer**: span-of-control inflation — the megamanager era, average US manager now overseeing 12 reports (up from ~6), Meta at 50:1.
- **Analytical layer**: Neil Thompson's expertise paradox — the decisive question for every AI-affected profession is whether the automated tasks were administrative scaffolding or the expert core.
- **Historical layer**: Morgan Stanley analysis of five prior US innovation waves; gains materialize years after disruption; distribution depends on policy (Great Compression vs. post-1980 inequality).

This domain connects to frontier AI (same capability wave driving coding agents and cybersecurity is restructuring management) and to deep work/flow (span-of-control inflation is a structural attacker of the conditions needed for expert-level work).

## Open Questions

- Which robotics subfield will be the focus? (perception, manipulation, mobile robotics, a specific industry?)
- Career path specifics: what skills are needed for each role beyond the high-level taxonomy?
- At what point does this wiki need a search tool beyond index.md?
- Edge AI hardware specifics: which chip families (NVIDIA Jetson, Coral TPU, microNPUs) and what are their capability profiles?
- In cybersecurity, does AI favor attackers, defenders, or simply the fastest adopters on either side?
- For managers specifically: are they living through the radiologist scenario or the taxi-driver scenario?

---

*Last updated: 2026-04-08 — after ingest: megamanager-era-how-many-direct-reports-ai-middle-management*
