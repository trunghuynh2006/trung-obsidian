# Wiki Overview

High-level synthesis of everything in this wiki. Updated after each ingest.

---

## What this wiki is about

This wiki spans seven domains: **knowledge management** (LLM Wiki pattern), **robotics education** (how to navigate a complex multidisciplinary field), **productivity/focus** (deep work, flow, and the attention economy), **AI+IoT systems** (edge AI architecture and industrial applications), **frontier AI capability/safety/security** (coding agents, alignment, and AI-enabled cybersecurity), **AI + labor markets** (how AI restructures work, expertise, and organizational design), and **behavioral economics / applied microeconomics** (incentives, conventional wisdom, expert exploitation, and measurement methodology). These connect: all seven are about how intelligence — human or artificial — compounds through tools and systems, and about what kinds of discipline are needed when capability starts moving faster than human review. The robotics branch now has a clearer infrastructure story as well: real-world AI needs not just models and actuators, but reliable spatial grounding.

## Current Thesis

Four compounding ideas, now converging:

1. **LLM Wiki pattern** — LLMs can maintain a persistent, compounding knowledge base better than RAG or human bookkeeping alone. The schema (CLAUDE.md) is the key: it gives the LLM discipline across sessions.

2. **Problem-driven learning** — In fields like robotics, where knowledge is vast and multidisciplinary, the only workable path is following problems rather than roadmaps. Deep expertise is built through iteration on real builds, not pre-specified curricula.

3. **Deep work and flow** — Sustained focus is a learnable skill under systemic attack from the attention economy. Flow (Csikszentmihalyi) emerges when challenge matches skill; deep work (Newport) is the deliberate practice that creates those conditions.

4. **Frontier AI changes both throughput and risk** — The same coding-capable systems that raise productivity also create new review, safety, and security burdens. AI coding agents increase code volume; emergent misalignment shows character-level safety can fail in non-obvious ways; AI cybersecurity collapses the time windows in the offense-defense race.

5. **The expertise paradox governs AI's labor market effects** — Whether AI augments or hollows a profession depends on which tasks it automates. Eliminating administrative scaffolding raises wages and concentrates expert work; eliminating the expert core deskills and depresses wages. This is the decisive variable for every profession AI is touching — managers, radiologists, software developers, and beyond.

6. **Expert incentive misalignment is the demand-side complement** — Even before AI, experts exploit informational monopolies against clients. Levitt (Freakonomics) measures this empirically: real estate agents sell their own homes for 3% more and hold them 10 days longer. AI erodes the informational asymmetry that enables exploitation — not by automating expert tasks, but by giving clients transparency. This creates a third scenario beyond Thompson's two: *disintermediation* — the expert's skills remain intact, their leverage does not.

**The convergence point:** Problem-driven learning naturally creates the challenge-skill balance that induces flow. Deep work provides the uninterrupted blocks needed for both. The LLM Wiki reduces the cognitive overhead of knowledge management. The frontier-AI sources add the missing caution: every capability gain creates a corresponding need for review, alignment, and security discipline. The labor-market domain adds a further dimension: capability gains do not distribute automatically — policy, institutions, and organizational design determine whether workers are augmented or hollowed. And the behavioral-economics domain adds the sharpest edge: experts aren't neutral agents working on your behalf. They respond to incentives. AI restructures those incentives by eroding informational asymmetry — which may do as much for clients as automating expert tasks directly. These are all anti-fragmentation ideas, but they now come with an explicit governance problem and a trust problem.

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

## Robotics Coverage (4 sources in)

Two layers now established:
- **Philosophy layer**: problem-driven learning, why roadmaps fail, the multidisciplinary trap — from the practitioner guide.
- **Reference layer**: career paths + industry stats, robot types taxonomy, hardware component anatomy — from the Playto Labs guide.
- **Spatial infrastructure layer**: machine-readable maps, visual localization, and geospatial world models as deployment substrate for physical AI — from the Niantic Spatial source.

The three layers complement each other. The philosophy tells you *how to learn*; the reference tells you *what the landscape looks like*; the infrastructure layer tells you what real-world deployment still requires after reasoning and control are in place.

This new layer sharpens the meaning of [[wiki/concepts/physical-ai]]. The missing ingredient is not always "more intelligence." Sometimes it is a better representation of the world: captured environments, reusable 3D assets, and localization systems that let robots stay oriented once they leave simulation. That connects the robotics domain more tightly to the AI+IoT domain, where physical deployment constraints already mattered.

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

## AI + Labor Markets Coverage (2 sources in)

New domain established around the expertise paradox and organizational restructuring:
- **Structural layer**: span-of-control inflation — the megamanager era, average US manager now overseeing 12 reports (up from ~6), Meta at 50:1.
- **Analytical layer**: Neil Thompson's expertise paradox — the decisive question for every AI-affected profession is whether the automated tasks were administrative scaffolding or the expert core.
- **Historical layer**: Morgan Stanley analysis of five prior US innovation waves; gains materialize years after disruption; distribution depends on policy (Great Compression vs. post-1980 inequality).
- **Strategic layer**: transformation under uncertainty — in AI-accelerated markets, waiting for clarity is itself a costly choice; firms need strategic pacing, clear ownership, and AI-native workflow redesign.

This domain connects to frontier AI (same capability wave driving coding agents and cybersecurity is restructuring management) and to deep work/flow (span-of-control inflation is a structural attacker of the conditions needed for expert-level work). The KPMG/Fast Company source adds a management-governance angle: beyond what AI does to jobs, there is the separate question of how organizations should move while those changes are unfolding. The article's answer is not "faster at all costs" but "trade certainty-seeking for disciplined maneuverability."

## Behavioral Economics / Applied Microeconomics Coverage (1 source in)

New domain established via Freakonomics introduction:
- **Methodological layer**: economics as measurement science; correlation vs. causation; natural experiments; the controlled comparison method
- **Incentive layer**: expert incentive misalignment — informational asymmetry enables exploitation; empirically measurable via self-vs-client comparisons
- **Epistemological layer**: conventional wisdom — how false beliefs form, why experts defend them, and how data dismantles them

This domain connects directly to the expertise paradox (Thompson's supply-side + Levitt's demand-side = a complete theory of expertise under AI pressure) and to the frontier-AI security domain (informational asymmetry as a structural feature of complex systems, not just expert-client relationships).

## Open Questions

- Which robotics subfield will be the focus? (perception, manipulation, mobile robotics, a specific industry?)
- Which spatial-data and localization platforms will matter most for real-world robotics deployment?
- Career path specifics: what skills are needed for each role beyond the high-level taxonomy?
- At what point does this wiki need a search tool beyond index.md?
- Edge AI hardware specifics: which chip families (NVIDIA Jetson, Coral TPU, microNPUs) and what are their capability profiles?
- In cybersecurity, does AI favor attackers, defenders, or simply the fastest adopters on either side?
- For managers specifically: are they living through the radiologist scenario or the taxi-driver scenario?
- In the AI era, will organizational advantage come more from model access or from strategic pacing and workflow redesign?
- **New (Freakonomics):** Which professions are being disintermediated by AI transparency tools, as opposed to having their tasks directly automated?
- **New (Freakonomics):** As more Freakonomics chapters are ingested, which of the five theses gets the most empirical weight?

---

*Last updated: 2026-04-08 — after ingest: this-is-the-biggest-risk-a-company-can-take-during-the-age-of-ai*
