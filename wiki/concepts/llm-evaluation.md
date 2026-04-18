---
date: 2026-04-11
type: concept
name: LLM Evaluation
aliases: [model evaluation, evaluation framework, evals]
tags: [llm, evaluation, governance, monitoring, compliance]
sources: 1
---

# LLM Evaluation

## Definition

The structured process of measuring whether a language model's behavior meets the task, policy, and risk requirements of its intended deployment, using task-grounded criteria, representative datasets, scoring rubrics, human review, and ongoing monitoring across the model lifecycle.

## Detail

The current source argues that evaluation should be understood less as a one-time benchmark exercise and more as a control system for deployed model behavior. In enterprise settings, the relevant question is not simply whether a model is generally capable, but whether it behaves acceptably inside the operational contexts where it will be used: customer communication, documentation, compliance-sensitive workflows, decision support, or other settings where output errors have downstream consequences.

That makes evaluation inherently lifecycle-oriented. Criteria have to be defined from the real task profile, datasets need to reflect routine use plus edge cases and adversarial prompts, and scoring has to combine automated checks with human review where judgment, tone, or policy nuance matters. Evaluation then continues after deployment through monitoring, reviewer calibration, regression checks, and versioned audit records.

In this framing, evaluation is the practical mechanism that turns AI governance into something operational. Naming an executive owner matters, but so does having a documented way to decide whether a model version should ship, whether behavior has drifted, and whether risk is still inside acceptable bounds.

## Evidence & Examples

- The source says operational performance criteria should map directly to the model's deployment task profile rather than to generic academic benchmarks [[wiki/sources/how-to-run-llm-evaluation-for-better-ai-performance]]
- Evaluation datasets are described as needing routine prompts, ambiguous requests, policy edge cases, and adversarial inputs [[wiki/sources/how-to-run-llm-evaluation-for-better-ai-performance]]
- Automated metrics are described as insufficient for contextual judgment, tone alignment, and policy-sensitive reasoning without structured human review [[wiki/sources/how-to-run-llm-evaluation-for-better-ai-performance]]
- Continuous evaluation is described as necessary for detecting regressions, distribution shift, and policy drift as models change [[wiki/sources/how-to-run-llm-evaluation-for-better-ai-performance]]
- Versioned records, change logs, and risk assessments are framed as part of audit readiness and governance documentation [[wiki/sources/how-to-run-llm-evaluation-for-better-ai-performance]]

## Connections

- [[wiki/concepts/ai-governance]] — evaluation is one of the concrete operating mechanisms that makes governance real
- [[wiki/concepts/agentic-ai]] — the more autonomy a system has, the more important explicit behavioral evaluation becomes
- [[wiki/concepts/ai-coding-agents]] — rapid model-assisted output increases the premium on review and measurable quality control
- [[wiki/concepts/ai-workforce-readiness]] — domain experts are part of evaluation pipelines, not only end-user adoption

## Two Evaluation Paradigms

The wiki now has evidence for two distinct evaluation paradigms with different goals:

1. **Enterprise deployment evaluation** (this concept) — is this specific model behaving acceptably inside this deployment context? Criteria are task-grounded, criteria-specific, and change slowly. The model is treated as a black box to be monitored.

2. **Frontier capability tracking** (see [[wiki/concepts/ai-benchmarking]]) — how far can the current leading models now go as autonomous agents? Criteria are task-length benchmarks; the trend line across model generations is the signal. METR's time-horizon chart is the canonical example.

These paradigms are not in conflict — they answer different questions — but they are often conflated. Enterprise eval teams asking "is our model behaving acceptably?" are doing a different job than capability researchers asking "where is the frontier moving?" [[wiki/sources/how-do-you-measure-an-ai-boom]]

A further complication for both paradigms: models powerful enough to exhibit [[wiki/concepts/sandbagging]] (intentional underperformance) or [[wiki/concepts/situational-awareness-ai]] make all evaluation results provisional lower bounds rather than true capability measures.

## Contradictions

- No contradiction captured yet; the current source set does not compare lightweight automated eval regimes against heavier human-in-the-loop evaluation programs or show which combinations work best by use case.
- METR's own productivity RCT swung from −19% to +20% in successive studies, illustrating how sensitive evaluation results are to experimental design even for the same population of users. [[wiki/sources/how-do-you-measure-an-ai-boom]]

## Sources

- [[wiki/sources/how-to-run-llm-evaluation-for-better-ai-performance]] — frames evaluation as a governance function with task-grounded criteria, human review, and continuous monitoring
- [[wiki/sources/how-do-you-measure-an-ai-boom]] — METR's time-horizon methodology as a contrasting capability-tracking paradigm; sandbagging as an evaluation integrity problem
