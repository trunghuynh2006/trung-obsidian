---
date: 2026-05-07
type: concept
name: AI Development Practices
aliases: [AI-assisted development techniques, AI coding practices]
tags: [software-engineering, ai-coding, tdd, ddd, practices]
sources: 1
---

# AI Development Practices

## Definition

A set of software engineering techniques — rooted in classical fundamentals — that constrain AI code generation to prevent [[wiki/concepts/software-entropy]] and maintain structural coherence as AI takes on more implementation work. Each technique addresses a specific failure mode of unconstrained AI-assisted development.

## Detail

Matt Pocock identifies four failure modes and a corresponding technique for each:

### 1. Design Concept Misalignment → "Grill Me" Technique

**Failure mode**: developer feeds AI a rough spec; AI builds something technically functional but architecturally misaligned. Neither party shared a design concept before building.

**Technique**: reverse the interview. Ask the AI to question you — challenge your assumptions, expose gaps in the spec, surface ambiguities — until a shared design concept is established. Only then start building. The AI's role here is as a Socratic interlocutor, not a code generator.

### 2. Vocabulary Drift → Ubiquitous Language File

**Failure mode**: developer and AI use different terms for the same concept, or the same term for different concepts. Over multiple sessions, prompts become imprecise and AI output becomes verbose and misaligned.

**Technique**: maintain a shared vocabulary markdown file — a glossary of domain concepts and their canonical names, rooted in Domain-Driven Design principles. Anchor every AI prompt to this file. The AI produces code that uses the vocabulary correctly; the developer enforces the vocabulary at every boundary.

### 3. Undisciplined Large Steps → TDD as Speed Limit

**Failure mode**: AI takes large, sweeping implementation steps — modifying many parts of the system at once, skipping incremental validation. Bugs compound before they are caught; the change becomes hard to understand or reverse.

**Technique**: apply Test-Driven Development. Write a failing test first; have the AI make only the change needed to pass that test. TDD forces AI to operate in tight, verifiable increments. The test suite is the speed limit: AI cannot outrun what can be verified. This is TDD-as-discipline rather than TDD-for-coverage.

### 4. Shallow Module Proliferation → Deep Module Design

**Failure mode**: AI generates shallow modules — many small, tangled units with complex interfaces that leak implementation detail. The architecture fragments; cognitive load rises; testing becomes difficult.

**Technique**: design [[wiki/concepts/deep-modules]] — simple interfaces, complex implementations. The human developer owns the interface design (strategic); the AI implements the internals (tactical). This is gray box delegation: the developer controls the shape; the AI fills the content.

## The Underlying Pattern

All four techniques share a structure: the human sets a constraint (shared concept, shared vocabulary, test, interface); the AI operates within that constraint. When the human fails to set the constraint, AI fills the gap with its own defaults — and those defaults optimize for local correctness, not global coherence. Fundamentals are not a substitute for AI; they are the scaffolding that keeps AI output composable.

## Connections

- [[wiki/concepts/software-entropy]] — the shared failure mode all four techniques prevent
- [[wiki/concepts/deep-modules]] — the architectural technique in item 4; detailed separately
- [[wiki/concepts/ai-coding-agents]] — the tools these practices apply to
- [[wiki/concepts/schema-driven-agents]] — strong structural parallel: just as CLAUDE.md disciplines an LLM across sessions (shared vocabulary, defined operations, enforced format), a ubiquitous language file + TDD + interface contracts discipline an AI coding agent across a codebase
- [[wiki/concepts/llm-evaluation]] — parallel concern: evaluation is the system-level equivalent of TDD's tight feedback loop; both prevent AI output from drifting outside verified bounds
- [[wiki/entities/matt-pocock]] — source author

## Sources

- [[wiki/sources/software-fundamentals-matter-more-than-ever]] — primary statement of all four techniques and their failure modes
