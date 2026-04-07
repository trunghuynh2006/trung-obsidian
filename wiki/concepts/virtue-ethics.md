---
type: concept
name: Virtue Ethics
aliases: [virtue theory, aretaic ethics, unity of virtues]
tags: [philosophy, ethics, ai, alignment, character]
sources: 1
---

# Virtue Ethics

## Definition

A family of moral philosophy that centers *character* rather than rules (deontology) or outcomes (consequentialism). The central question is not "what rule applies here?" or "what maximizes good outcomes?" but "what would a person of good character do?"

The key claim: virtues are not isolated traits. They are deeply interconnected — unified by a shared capacity for practical wisdom (*phronesis*). You cannot truly possess courage without also having justice, temperance, and wisdom. A person genuinely good in one respect tends to be good in others.

## Historical Development

**Ancient foundation:**
- **Plato**: all virtues are ultimately one thing — knowledge of the good. Vice is a form of ignorance.
- **Aristotle**: virtues are unified through *phronesis* (practical wisdom). A soldier who fights from fear of disgrace rather than noble understanding is only *apparently* brave — and probably only apparently virtuous elsewhere too.
- **Stoics**: the virtues are inseparable; you possess them all or none.
- **Augustine / Aquinas**: carried the unified-virtue view into Catholic theology.

**Decline:**
Virtue ethics fell out of favor ~400 years ago as deontology (Kant) and consequentialism (Bentham, Mill) rose to dominance. The "compartmentalized" view replaced it: people can be good and bad in any mixture; character is not unified.

**Revival:**
Late 20th century. British philosophers (Philippa Foot, G.E.M. Anscombe, Alasdair MacIntyre) revived virtue ethics partly in response to WWII — arguing that deontology and consequentialism couldn't adequately account for the nature of those atrocities. Foot argued that imprudence is in the same class as wickedness.

## The LLM Connection

The [[wiki/concepts/emergent-misalignment]] finding provides computational evidence for virtue ethics' core claim — at least in LLMs. Fine-tuning a model to write bad code corrupted its *entire character* across unrelated domains. The model couldn't compartmentalize its badness.

The mechanism is mathematical: consistent character is computationally cheaper than compartmentalized character. Being consistently bad is stabler than being selectively bad.

Anthropic has explicitly built Claude's character on Aristotelian virtue ethics, with house philosopher Amanda Askell designing Claude's foundational character guide around *practical wisdom*. [[wiki/entities/amanda-askell]]

## Virtue Ethics vs. Other Frameworks

| Framework | Center | Question asked |
|---|---|---|
| **Virtue ethics** | Character | What would a person of good character do? |
| **Deontology** | Rules | What rule applies? |
| **Consequentialism** | Outcomes | What maximizes good results? |

Virtue ethics is less prescriptive than the other two — it requires judgment rather than rule-following. This is why it maps naturally onto LLMs, which also operate through judgment rather than explicit rules.

## Connections

- [[wiki/concepts/emergent-misalignment]] — provides computational evidence for the unity-of-virtues claim in LLMs.
- [[wiki/entities/anthropic]] — betting on virtue ethics as the foundation for AI alignment.
- [[wiki/entities/amanda-askell]] — designed Claude's character around Aristotelian practical wisdom.

## Sources

- [[wiki/sources/ai-chatbots-virtue-vice]] — places virtue ethics in dialogue with emergent misalignment; historical overview and philosophical argument.
