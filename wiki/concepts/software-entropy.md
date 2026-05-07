---
date: 2026-05-07
type: concept
name: Software Entropy
aliases: [codebase entropy, code rot, software rot]
tags: [software-engineering, ai-coding, architecture, quality]
sources: 1
---

# Software Entropy

## Definition

The progressive structural degradation of a codebase — each change makes the next change slightly harder, the system becomes less coherent over time, and the cost of modification grows. In the AI era, software entropy is specifically accelerated by specs-to-code development: generating code from specifications with minimal structural discipline, so each AI-generated layer compounds the disorganization of the last.

## Detail

Entropy in software is not primarily about bugs; it is about structural properties. A codebase suffering entropy may still run correctly while becoming increasingly hard to reason about, test, or extend. The mechanisms are:

- **Naming drift**: concepts called different things in different places, no shared vocabulary
- **Shallow modules proliferating**: many tiny, complex units with leaky abstractions
- **Undisciplined large steps**: changes that modify many parts of the system at once, making understanding difficult
- **Design concept misalignment**: the built system no longer matches anyone's mental model of what it should be

AI code generation accelerates all four mechanisms because AI optimizes for local correctness (does this unit work?) rather than global coherence (does this unit fit the architecture?). Without structural discipline imposed by the human developer, each AI-generated change can introduce small violations that compound over time.

The remedy is not less AI, but AI constrained by human-maintained structure: shared vocabulary, deep module boundaries, small testable increments, and explicit design concepts. See [[wiki/concepts/ai-development-practices]].

## Evidence & Examples

- Matt Pocock's warning about specs-to-code movement: relying solely on AI to generate code from specs leads to software entropy [[wiki/sources/software-fundamentals-matter-more-than-ever]]
- Code overload data: financial services firm at 1M line review backlog after AI adoption — unchecked entropy compounds when review cannot keep pace [[wiki/concepts/ai-coding-agents]] / [[wiki/sources/ai-code-overload]]

## Connections

- [[wiki/concepts/ai-development-practices]] — the four techniques that counteract software entropy in AI-assisted development
- [[wiki/concepts/deep-modules]] — the architectural pattern that provides structural resistance to entropy
- [[wiki/concepts/ai-coding-agents]] — entropy is the structural failure mode that accompanies the volume/security failure modes already documented
- [[wiki/concepts/loose-coupling]] — the EAI principle that addresses a related structural concern: each coupling dimension (platform, time, data format) is an entropy vector in integration systems

## Sources

- [[wiki/sources/software-fundamentals-matter-more-than-ever]] — defines entropy as the central failure mode of unconstrained AI code generation
