---
date: 2026-05-07
type: source
title: "Matt Pocock: Software Fundamentals Matter More Than Ever"
source_file: raw/sources/software-fundamentals-matter-more-than-ever.md
date_ingested: 2026-05-07
tags: [software-engineering, ai-coding, tdd, architecture, practices]
---

# Matt Pocock: Software Fundamentals Matter More Than Ever

**Source:** [[raw/sources/software-fundamentals-matter-more-than-ever]]
**Ingested:** 2026-05-07
**Tags:** #software-engineering #ai-coding #tdd #architecture #practices

## Summary

Matt Pocock argues that the "specs-to-code" movement — feeding AI a specification and accepting the output with minimal structural oversight — produces software entropy: a codebase that degrades progressively with each AI-generated change, becoming harder and harder to modify. The failure is not that AI writes bad code in isolation; it is that AI code generation, left unshaped by engineering fundamentals, erodes the structural properties that make a system maintainable over time.

Pocock maps four specific failure modes of AI-assisted development and pairs each with a technique rooted in classical software engineering: design misalignment (solved by the "grill me" technique), vocabulary drift (solved by a shared ubiquitous language markdown file), large undisciplined steps (solved by TDD as a feedback loop enforcer), and shallow module architecture (solved by designing deep modules that give AI a clean delegation boundary).

The unifying thesis is a division of labor: AI is an excellent tactical programmer — it can implement a well-specified unit, fill in an interface, or generate tests for a named behavior. The human developer must remain the strategic architect — defining module boundaries, naming concepts, deciding what gets built and why. When that division collapses and AI is asked to make strategic decisions it cannot ground in the actual system, entropy follows.

## Key Points

- **Software entropy**: specs-to-code AI reliance produces codebases that get progressively harder to change — each generation slightly worse than the last.
- **"Grill me" technique**: instead of feeding AI a spec, have the AI interview you with questions until a shared design concept emerges. Prevents building the wrong thing.
- **Ubiquitous language with AI**: maintain a shared vocabulary markdown file; root it in Domain-Driven Design; anchor all AI prompts to it. Prevents verbosity and concept drift.
- **TDD as AI speed limit**: test-driven development forces AI to take small, testable steps rather than generating large opaque blobs. Acts as a feedback loop that catches bugs early.
- **Deep modules as delegation boundary**: human designs the interface (simple, stable, intentional); AI implements the internals. The module boundary is where human strategic judgment ends and AI tactical execution begins.
- **Gray box delegation**: the human treats the module as a gray box — controls the interface, delegates the implementation. Saves cognitive load for architecture.
- **AI = tactical programmer; human = strategic architect**: the division of labor that all four techniques enforce.

## Connections

- [[wiki/concepts/software-entropy]] — central failure mode motivating all four techniques
- [[wiki/concepts/deep-modules]] — the architectural principle Pocock uses as the AI delegation boundary
- [[wiki/concepts/ai-development-practices]] — the four concrete techniques (grill me, ubiquitous language, TDD feedback loop, gray box delegation)
- [[wiki/concepts/ai-coding-agents]] — this source adds the entropy risk angle to the existing code-overload and security-gap picture
- [[wiki/concepts/schema-driven-agents]] — loose parallel: just as CLAUDE.md disciplines an LLM wiki agent, a ubiquitous language file disciplines an AI coding agent
- [[wiki/entities/matt-pocock]] — speaker and source author

## Quotes

> "While AI is an excellent 'tactical programmer,' the human developer must act as the strategic architect, constantly investing in the system's design."
