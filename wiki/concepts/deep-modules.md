---
date: 2026-05-07
type: concept
name: Deep Modules
aliases: [deep module design]
tags: [software-engineering, architecture, ai-coding, cognitive-load]
sources: 1
---

# Deep Modules

## Definition

A module design principle from John Ousterhout's *A Philosophy of Software Design*: a deep module has a **simple interface** hiding a **complex implementation**. The depth metaphor is a ratio — the more complexity hidden behind a clean surface, the "deeper" the module. The opposite is a shallow module: a tiny, tangled unit with a complex or leaky interface that forces callers to understand its internals.

## Detail

Deep modules reduce cognitive load because callers only need to understand the interface, not the implementation. The entire complexity of the implementation is contained behind a stable boundary. This property has two downstream benefits:

1. **Testability**: simple interfaces are easy to test against; complex internals can be verified without exposing them.
2. **Replaceability**: implementations can change without callers knowing, as long as the interface holds.

**Applied to AI-assisted development**, deep modules become the mechanism for human-AI division of labor. The human developer designs the module interface — a strategic decision about what the module should do and how it presents itself to the rest of the system. The AI implements the internals — a tactical task of filling in the behavior behind a well-specified surface. Matt Pocock describes this as "gray box delegation": the human controls the shape; the AI fills the content.

This is also a cognitive load management strategy. By treating modules as gray boxes at the system level, the developer preserves mental energy for architectural decisions and delegates implementation detail to the AI. The interface *is* the spec the AI operates against; because it is explicitly designed rather than AI-generated, it does not itself contribute to [[wiki/concepts/software-entropy]].

## Evidence & Examples

- Pocock applies Ousterhout's deep module principle directly to AI delegation: human designs interface, AI implements internals [[wiki/sources/software-fundamentals-matter-more-than-ever]]
- Comparison: shallow modules ("tiny, complex blobs") are both harder to test and give AI too much structural decision-making authority

## Connections

- [[wiki/concepts/software-entropy]] — deep module design is the architectural remedy for entropy; stable interfaces prevent concept drift and compounding disorganization
- [[wiki/concepts/ai-development-practices]] — deep modules are one of the four AI-assisted development techniques
- [[wiki/concepts/loose-coupling]] — deep modules reduce coupling by hiding implementation behind stable interfaces; the EAI counterpart to the same principle
- [[wiki/concepts/message-endpoint]] — loose structural analogy: a well-defined channel adapter hides integration complexity behind a clean boundary, as a deep module hides implementation complexity behind a clean interface

## Sources

- [[wiki/sources/software-fundamentals-matter-more-than-ever]] — Pocock applies Ousterhout's principle as the AI delegation boundary mechanism
