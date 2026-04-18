# Wiki Overview

High-level synthesis of everything in this wiki. Updated after each ingest.

---

## What this wiki is about

This wiki spans eight domains: **knowledge management** (LLM Wiki pattern), **robotics education** (how to navigate a complex multidisciplinary field), **productivity/focus** (deep work, flow, and the attention economy), **AI+IoT systems** (edge AI architecture and industrial applications), **frontier AI capability/safety/security** (coding agents, alignment, and AI-enabled cybersecurity), **AI + labor markets** (how AI restructures work, expertise, and organizational design), **behavioral economics / applied microeconomics** (incentives, conventional wisdom, expert exploitation, and measurement methodology), and **enterprise integration / software architecture** (messaging patterns, loose coupling, and the vocabulary of distributed systems design). These connect: all seven are about how intelligence — human or artificial — compounds through tools and systems, and about what kinds of discipline are needed when capability starts moving faster than human review. The robotics branch now has a clearer infrastructure story as well: real-world AI needs not just models and actuators, but reliable spatial grounding.

## Current Thesis

Four compounding ideas, now converging:

1. **LLM Wiki pattern** — LLMs can maintain a persistent, compounding knowledge base better than RAG or human bookkeeping alone. The schema (CLAUDE.md) is the key: it gives the LLM discipline across sessions.

2. **Problem-driven learning** — In fields like robotics, where knowledge is vast and multidisciplinary, the only workable path is following problems rather than roadmaps. Deep expertise is built through iteration on real builds, not pre-specified curricula. The new ultralearning source generalizes this beyond robotics and adds tactical machinery around it: map the terrain first, practice directly, isolate bottlenecks, retrieve from memory, and use feedback aggressively.

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
- **Directness over abstraction** — real skill comes fastest from doing the thing itself, not studying proxies for it too long.
- **Acceleration vs. control** — AI increases throughput in code and cybersecurity faster than institutions can review, secure, or govern it.

## Major Entities

- [[wiki/entities/obsidian]] — the reading interface for this wiki
- [[wiki/entities/vannevar-bush]] — intellectual ancestor of LLM Wiki (Memex, 1945)
- [[wiki/entities/first-robotics]] — best starting environment for young roboticists (confirmed by 2 sources)
- [[wiki/entities/arduino]] — canonical beginner hardware platform
- [[wiki/entities/ros2]] — industry-standard robotics middleware

## Robotics Coverage (8 sources in)

Seven layers now established:
- **Philosophy layer**: problem-driven learning, why roadmaps fail, the multidisciplinary trap — from the practitioner guide.
- **Reference layer**: career paths + industry stats, robot types taxonomy, hardware component anatomy — from the Playto Labs guide.
- **Spatial infrastructure layer**: machine-readable maps, visual localization, and geospatial world models as deployment substrate for physical AI — from the Niantic Spatial source.
- **Operational-memory layer**: email, cloud files, and collaboration trails as part of robotics continuity, auditability, and recovery readiness — from the Microsoft 365 backup source.
- **Environmental-awareness layer**: weather and forecast inputs as live decision context for robots and outdoor automation — from the weather-intelligence source.
- **Reasoning layer**: foundation models integrated directly into deployed robots, enabling transition from detection to reasoning — from the Boston Dynamics / Google DeepMind source.
- **Decentralized swarm layer**: no central controller, no foundation model — emergent construction and dismantling from simple local rules and environmental feedback, using stigmergy as the coordination mechanism — from the Harvard SEAS RAnts source.

The seven layers complement each other. The philosophy tells you *how to learn*; the reference tells you *what the landscape looks like*; the infrastructure layer tells you what real-world deployment still requires after reasoning and control are in place; the operational-memory layer explains why recoverable decision context matters once real teams, vendors, audits, and incidents enter the picture; the environmental-awareness layer explains why even well-localized systems still need structured external data once the world starts changing around them.

This new layer sharpens the meaning of [[wiki/concepts/physical-ai]]. The missing ingredient is not always "more intelligence." Sometimes it is a better representation of the world: captured environments, reusable 3D assets, and localization systems that let robots stay oriented once they leave simulation. That connects the robotics domain more tightly to the AI+IoT domain, where physical deployment constraints already mattered.

The Microsoft 365 backup source adds a quieter but important correction to the robotics branch: the data substrate of robotics is not only CAD, code, and machine telemetry. It is also the collaboration layer that stores approvals, vendor coordination, test discussion, and rationale. In practice, recovery gaps there become operational gaps. That ties robotics more tightly to security and governance concerns: resilience in industrial settings depends on restoring decision context, not just files in isolation.

The Harvard SEAS RAnts source adds a new architectural dimension to the robotics branch by introducing the opposite end of the design spectrum from foundation-model-based Physical AI. Where Gemini Robotics-ER locates intelligence in a single sophisticated agent, the RAnts swarm locates it in the environment: each robot is nearly brainless, but the collective feedback loop between hundreds of robots and a shared light-field medium (photormones) produces adaptive construction or dismantling on demand. The mechanism is [[wiki/concepts/stigmergy]] — indirect coordination through environmental modification — implemented robotically via trapping instability as the nucleation mechanism. The key conceptual contribution is [[wiki/concepts/exbodied-intelligence]]: a new term for collective cognition distributed into an evolving shared environment rather than any individual body. This sharpens the Physical AI picture into a genuine design spectrum: one axis is agent sophistication (minimal ↔ foundation model); another is intelligence location (exbodied / environmental ↔ embodied / in-agent). Real deployments will likely combine both approaches depending on the task class.

**New open questions from this source:**
- At what task complexity does the swarm approach break down and the foundation-model approach become necessary?
- Can photormone-style environmental encoding be combined with embodied-reasoning agents to get robustness *and* generalization?
- How does trapping instability generalize to 3D construction environments or dynamic obstacles?

The Boston Dynamics / DeepMind source adds the sharpest layer yet to the robotics branch: a named, production-deployed instance of a frontier foundation model (Gemini Robotics-ER 1.6) running inside an industrial robot platform (Spot/Orbit/AIVI). The central claim is that the robotics field has crossed a detection-to-reasoning threshold. Detection-based systems require pre-specified anomaly classes; reasoning-based systems answer novel questions about facility state. The four capabilities that operationalize this — spatial relationship analysis, multi-camera synthesis, success detection, and instrument reading — collectively describe what "understanding" looks like in a physical AI system. Success detection is especially load-bearing: it closes the agentic feedback loop, allowing a robot to determine task completion without human confirmation. Without it, the system is not truly autonomous regardless of how sophisticated its perception is. This source introduces [[wiki/concepts/embodied-reasoning]] as a first-class wiki concept and grounds [[wiki/entities/boston-dynamics]], [[wiki/entities/google-deepmind]], [[wiki/entities/spot-robot]], and [[wiki/entities/gemini-robotics]] as entities. A notable open question: the deployment is cloud-based (not edge), contrasting with the edge-AI architecture dominant in IIoT. This tradeoff — reasoning power vs. connectivity dependence — is now an active tension in the Physical AI picture.

The weather-intelligence source adds a complementary correction: perception and localization are not enough by themselves. Real-world automation also needs external environmental awareness. A robot may know where it is and still make poor choices if it cannot account for wind, rain, temperature shifts, or short-horizon forecasts. That pushes the robotics branch toward a fuller deployment model: simulation, spatial grounding, operational memory, and environment-aware adaptation.

## AI+IoT Coverage (4 sources in)

A new domain now established around the edge/on-device AI architecture and industrial applications:
- **Architecture layer**: edge AI (model quantization, pruning, distillation, edge chips), federated learning, the edge-cloud continuum
- **Application layer**: predictive maintenance, industrial QC, supply chain, energy arbitrage, multi-agent actor coordination
- **Workforce layer**: AI workforce readiness — role-specific training, AI literacy, data discipline, simulation practice, and adoption measurement as the human bottleneck in industrial deployment
- **Process/material layer**: CNC machining as a concrete production process where material choice, tolerances, tooling, and adaptive control meet the smart-factory story
- **External-environment layer**: weather intelligence as live operational input for exposed automation systems in logistics, energy, construction, mining, and delivery

This domain connects strongly to robotics (sensor/actuator nodes as AI-enhanced robot components) and to agentic AI (IIoT actor networks as deployed multi-agent physical systems). The LLM-as-interface pattern here — natural language queries to sensor networks, explainable actuator decisions — mirrors the LLM Wiki pattern: LLMs democratizing access to complex structured data.

The new workforce-training source adds an important correction to the earlier architecture-heavy picture: industrial AI adoption does not fail only at the model or systems level. It also fails at the workflow and skills level. Predictive dashboards, machine-vision outputs, and scheduling systems only matter if workers understand when to trust them, how to act on them, and who owns the resulting decisions. This creates a direct bridge between the AI+IoT domain and the AI + labor domain.

The new aluminum-CNC source brings the lens down another level, from plant-wide systems to the individual machine tool. Earlier industrial pages focused on sensing, maintenance, dashboards, and workforce training. This source grounds the same Industry 4.0 story in a specific production process: aluminum is attractive because it machines quickly while staying light and corrosion-resistant, and CNC cells are becoming more connected through smart tooling, sensor feedback, and adaptive parameter control. The source is vendor-biased and should not be over-weighted, but it adds a useful process-and-material layer to the industrial branch.

The new weather-intelligence source adds an outside-the-factory correction to that picture. Earlier IIoT pages mostly emphasized internal telemetry, plant systems, and asset data. This source argues that once automation leaves tightly controlled indoor settings, a system may need structured external environment data as much as it needs internal sensor data. That is an important broadening of the automation stack: reliable action depends not only on knowing machine state, but also on knowing changing world state.

## Frontier AI / Security Coverage (5 sources in)

Five layers are now visible inside the frontier-AI branch:
- **Productivity layer**: AI coding agents dramatically increase software output, but create a human review and security bottleneck.
- **Alignment layer**: emergent misalignment suggests character-level corruption can spread across domains, making safety a whole-model property rather than a per-task patching problem.
- **Cybersecurity layer**: the same models are now accelerating vulnerability discovery, defensive auditing, phishing, and AI-assisted intrusion workflows.
- **Nonproliferation layer**: some cyber-capable models may be strong enough that the central governance question shifts from "how should we use them?" to "who should be allowed to access them at all?"
- **Measurement layer**: METR's time-horizon chart tracks how autonomous AI agents are becoming, revealing an unexpectedly clean doubling trend — and exposing a new evaluation integrity problem: models capable of sandbagging and situational awareness make all capability benchmarks provisional.

Together these sources suggest a general pattern: frontier AI does not just automate tasks. It compresses time, widens blast radius, and raises the premium on governance. The same systems that make this wiki possible are also making security, oversight, and model character much more consequential.

The new Mythos/Glasswing source escalates this branch from acceleration to containment. Earlier cyber pages already suggested that AI was compressing offense-defense timelines. This source adds a sharper claim: a model may be able to find flaws across the shared software substrate of modern society so effectively that broad release itself becomes the problem. That introduces a new statecraft-level question for the wiki: can there be a meaningful regime of AI nonproliferation for cyber-capable models, or does capability diffusion outrun containment almost immediately?

The METR / time-horizon source adds a different kind of alarm: not the threat from AI misuse, but the threat from AI capability itself. METR provides what no prior source in this wiki has: a clear empirical trend line for autonomous AI progress, with a specific feared endpoint (intelligence explosion) and a named pathway (full automation of AI R&D). The doubling-every-3-4-months figure for task-completion length is now the wiki's sharpest single data point about the speed of change. Two sub-risks compound the picture: *sandbagging* (models gaming their own evaluations) and *covert capabilities* (models misbehaving while appearing to comply). Together these suggest that as frontier models improve, our ability to measure and contain them may be improving more slowly than the models themselves. [[wiki/sources/how-do-you-measure-an-ai-boom]]

## AI + Labor Markets Coverage (6 sources in)

New domain established around the expertise paradox and organizational restructuring:
- **Structural layer**: span-of-control inflation — the megamanager era, average US manager now overseeing 12 reports (up from ~6), Meta at 50:1.
- **Analytical layer**: Neil Thompson's expertise paradox — the decisive question for every AI-affected profession is whether the automated tasks were administrative scaffolding or the expert core.
- **Historical layer**: Morgan Stanley analysis of five prior US innovation waves; gains materialize years after disruption; distribution depends on policy (Great Compression vs. post-1980 inequality).
- **Strategic layer**: transformation under uncertainty — in AI-accelerated markets, waiting for clarity is itself a costly choice; firms need strategic pacing, clear ownership, and AI-native workflow redesign.
- **Governance layer**: the AI ownership vacuum — 60% of senior leaders report no one in their organization has clear ownership of AI. This is a structural consequence of AI's cross-cutting nature (people + systems + finance), not a failure of awareness. The fix is organizational design: either a cross-functional HR+IT+Finance alignment (three-step framework), or structural merger of roles (Moderna's CHRO+CIO combined into one executive).
- **Leadership-learning layer**: early AI advantage compounds mainly as judgment, confidence, and shared standards. Leaders need to model open experimentation, create guardrails, and normalize learning before teams build ungoverned habits on their own.
- **Operational-failure layer**: workslop — AI-generated output can look efficient at the draft stage while increasing total labor through downstream correction, clarification, and morale damage.

This domain connects to frontier AI (same capability wave driving coding agents and cybersecurity is restructuring management) and to deep work/flow (span-of-control inflation is a structural attacker of the conditions needed for expert-level work). The KPMG/Fast Company source adds a management-governance angle: beyond what AI does to jobs, there is the separate question of how organizations should move while those changes are unfolding. The article's answer is not "faster at all costs" but "trade certainty-seeking for disciplined maneuverability."

The new governance source sharpens a recurring tension in the wiki: AI capability consistently arrives faster than the institutions designed to govern it. This is visible in cybersecurity (AI compresses offense/defense timelines), in code review (AI raises output faster than security engineers can review it), and now in organizational design (AI restructures management before companies have decided who is responsible for managing that restructuring). The pattern is consistent: speed of capability > speed of governance.

The newer leadership/adoption source adds the missing behavioral layer beneath the org-chart discussion. Governance is not only about naming an executive owner. It is also about whether everyday AI use is visible, trained, and bounded by shared guardrails. That source also introduces a useful tension in the current wiki: one article pushes toward explicit ownership because "no one owns AI," while another says early progress became possible through committees and shared learning. The likely synthesis is accountable ownership plus structured learning forums, but the current sources do not test governance models empirically.

The new LLM-evaluation source extends that governance branch from ownership and guardrails into operational control. It argues that organizations do not really govern AI merely by naming an owner or setting usage policy. They also need versioned evaluation datasets, domain-expert review, regression monitoring, and auditable release records that tie model changes to measurable behavioral performance. This sharpens a useful distinction in the wiki: governance is not just organizational structure above the model, but control infrastructure around the model.

The new workslop source adds a missing operational reality check to this whole branch. Earlier sources mostly argued that firms should move before certainty arrives, name owners, and build learning loops. This source shows what happens when those principles are flattened into "make everyone use AI now." The result can be polished-looking low-trust output that shifts editing labor downstream, widens the executive-worker perception gap, and lowers morale. This sharpens the wiki's management thesis: the hard part of AI adoption is not willingness to move fast, but knowing where AI genuinely reduces work versus where it merely relocates work.

The Gallup/Walton/GSV Gen Z survey (2026) adds a **sentiment and generational layer** to the labor domain. The most important finding is that sentiment and adoption are diverging: ~50% of Gen Z uses AI daily or weekly (flat year-over-year), while hope fell from 27% to 18% and ~1/3 report anger. This is not ignorance-driven rejection — the youngest members are the most frequent users; the skeptics are older working adults with direct workplace experience. Their fears are overwhelmingly concentrated on the *expert-core automation* scenario: job replacement, creativity atrophy, deskilling. This is the taxi-driver scenario as lived experience. The data suggests that the expertise paradox is not just an academic framework but an accurate map of how a generation of workers *perceives* their own professional risk. The implication for workforce readiness is sharp: organizations cannot assume access drives adoption. Gen Z is arriving in the labor market already using AI, already skeptical, and already expecting to need AI fluency — but not yet trusting that AI will work in their favor. That is a new kind of readiness gap.

## Behavioral Economics / Applied Microeconomics Coverage (1 source in)

New domain established via Freakonomics introduction:
- **Methodological layer**: economics as measurement science; correlation vs. causation; natural experiments; the controlled comparison method
- **Incentive layer**: expert incentive misalignment — informational asymmetry enables exploitation; empirically measurable via self-vs-client comparisons
- **Epistemological layer**: conventional wisdom — how false beliefs form, why experts defend them, and how data dismantles them

This domain connects directly to the expertise paradox (Thompson's supply-side + Levitt's demand-side = a complete theory of expertise under AI pressure) and to the frontier-AI security domain (informational asymmetry as a structural feature of complex systems, not just expert-client relationships).

## Enterprise Integration / Software Architecture Coverage (1 source in)

New domain established via *Enterprise Integration Patterns* Ch1 (Hohpe & Woolf, 2004):

- **Problem-space layer**: why enterprise integration is fundamentally hard — political, control, standards, and operational dimensions; "simple integration" as oxymoron.
- **Principle layer**: loose coupling as the organizing design goal; four coupling dimensions (platform, location, time, data format); why RPC/CORBA-style "make remote look local" consistently fails.
- **Pattern catalog**: ~22 named patterns introduced through the WGRUS worked example, covering base infrastructure (Message, Channel, Endpoint), transformation (Translator, Canonical Data Model), routing (CBR, Filter, Recipient List), composition (Splitter, Aggregator, CMP), state (Message Store, Claim Check, Content Enricher), orchestration (Process Manager, Return Address), and monitoring (Wire Tap, Smart Proxy, Control Bus, Test Message).
- **Integration styles layer** (Ch2): formal pattern treatment of the four styles — File Transfer, Shared Database, Remote Procedure Invocation, Messaging — with seven decision criteria (coupling, simplicity, technology, data format, timeliness, data-vs-functionality, asynchronicity). The four styles form a progression of sophistication; Messaging is the recommended default for most enterprise integration.

The domain connects to [[wiki/concepts/agentic-ai]] — modern AI agents re-use many of the same architectural primitives (routing, message passing, orchestration, observability). It also connects to [[wiki/concepts/schema-driven-agents]]: the discipline of giving an AI a pattern vocabulary (CLAUDE.md) mirrors the role EIP patterns play in giving integration architects a shared design language. The EIP catalog is also directly relevant to [[wiki/entities/microsoft-pl400]] — Power Platform integrations and custom connectors use these patterns (channel adapters, message translators, publish-subscribe) even if they are not always labeled as such.

**Open Questions:**
- **New (EAI):** As more chapters are ingested, which pattern categories (routing, transformation, orchestration, monitoring) get the most nuanced treatment?
- **New (EAI):** How do modern event-driven architectures (Kafka, cloud event buses) map onto the 2004 EIP vocabulary — extensions, replacements, or the same patterns under new names?
- **New (EAI):** Where do agentic AI architectures diverge from EIP patterns, and where are they converging back to the same solutions?

## Open Questions

- Which robotics subfield will be the focus? (perception, manipulation, mobile robotics, a specific industry?)
- Which spatial-data and localization platforms will matter most for real-world robotics deployment?
- Career path specifics: what skills are needed for each role beyond the high-level taxonomy?
- How should ultralearning's metalearning step be balanced against the wiki's strong anti-roadmap stance?
- At what point does this wiki need a search tool beyond index.md?
- Edge AI hardware specifics: which chip families (NVIDIA Jetson, Coral TPU, microNPUs) and what are their capability profiles?
- Which training models best prepare incumbent industrial workers for AI-supported operations without disrupting production?
- For robotics firms, how should broad traceability/integrity expectations (for example IEC 62443 or NIS2) be translated into concrete backup and recovery standards for collaboration systems?
- How should real-world automation systems combine local sensor fusion with third-party weather intelligence without creating new failure modes or overdependence on external providers?
- In cybersecurity, does AI favor attackers, defenders, or simply the fastest adopters on either side?
- **New (AI cybersecurity):** Can controlled release of frontier cyber-capable models actually buy meaningful defensive time, or is proliferation effectively unavoidable?
- **New (AI cybersecurity):** If AI nonproliferation is necessary, what would count as a workable international regime rather than a corporate-public-relations gesture?
- **New (intelligence explosion):** Is the METR time-horizon trend line real or a measurement artifact? Nathan Witkin's January 2026 critique argues the latter — what would resolve this?
- **New (sandbagging):** If powerful models can strategically underperform on evaluations, what alternative methods can give reliable capability estimates?
- **New (covert capabilities):** Can AI monitors reliably detect AI misbehavior as model capability increases, or does the monitor face the same sandbagging/situational-awareness problem as the model being monitored?
- For managers specifically: are they living through the radiologist scenario or the taxi-driver scenario?
- In the AI era, will organizational advantage come more from model access or from strategic pacing and workflow redesign?
- **New (Freakonomics):** Which professions are being disintermediated by AI transparency tools, as opposed to having their tasks directly automated?
- **New (Freakonomics):** As more Freakonomics chapters are ingested, which of the five theses gets the most empirical weight?
- **New (AI governance):** Which governance model actually produces better AI outcomes — dedicated CAIO, merged HR+IT, cross-functional committee, or something else? No source yet compares models empirically.
- **New (AI governance):** Is the "cultural barrier" framing accurate, or is it a reframing that conveniently positions HR (and HR software vendors) as the solution?
- **New (AI governance):** What is the right balance between automated metrics, human review, and red-team-style adversarial testing for different classes of LLM deployment?
- **New (workslop):** How should organizations measure real AI productivity once correction labor, clarification work, and morale effects are included rather than hidden downstream?
- **New (Gen Z sentiment):** Is high usage + souring sentiment a transitional state that resolves as AI tools improve and labor market fears diminish — or is the expert-core threat real enough that Gen Z skepticism is a rational forward-looking signal?
- **New (Gen Z sentiment):** Can workforce readiness programs be designed to build *trust* as well as skill, given that the incoming cohort is already technically capable but motivationally skeptical?
- **New (embodied reasoning):** Cloud-based embodied reasoning (Gemini Robotics-ER) vs. edge-AI inference: at what connectivity threshold and latency budget does cloud reasoning become impractical for industrial robotics? Is there a hybrid architecture that captures both?
- **New (embodied reasoning):** Is "success detection" a general-purpose capability that transfers across task types, or does it require task-specific training for each inspection scenario?
- **New (swarm robotics):** At what task complexity does the swarm/stigmergy approach break down and the foundation-model approach become necessary?
- **New (swarm robotics):** Can photormone-style environmental encoding be combined with embodied-reasoning agents to get robustness *and* generalization?
- **New (swarm robotics):** How does exbodied intelligence scale beyond 2D construction? What kinds of environment encodings work for 3D or dynamic obstacle settings?

---

*Last updated: 2026-04-19 — after ingest: How Do You Measure an AI Boom? (NYT / METR) — measurement layer added to frontier AI coverage; 4 new concept pages (intelligence-explosion, ai-benchmarking, covert-capabilities, sandbagging); 4 new entity pages (metr, beth-barnes, chris-painter, ajeya-cotra); anthropic, openai, agentic-ai, llm-evaluation updated.*
