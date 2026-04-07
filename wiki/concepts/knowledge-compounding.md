---
type: concept
name: Knowledge Compounding
aliases: [compounding knowledge, accumulating synthesis]
tags: [knowledge-management, second-brain, llm-wiki]
sources: 1
---

# Knowledge Compounding

## Definition

The property of a knowledge system where each new piece of information makes the whole richer — not just by adding content, but by strengthening connections, resolving contradictions, and deepening synthesis across everything already present.

## Detail

Most information systems don't compound: a search engine returns results; a RAG system retrieves chunks; a note-taking app stores text. Each query or read starts fresh. Knowledge compounding requires a persistent, integrated representation that is actively updated as new information arrives.

In the LLM Wiki pattern, compounding happens at two levels:
1. **Ingestion compounding** — each new source is integrated into existing entity and concept pages, not just appended. The wiki's synthesis is updated, not just extended.
2. **Query compounding** — valuable analysis generated during a query session is filed back as an analysis page, becoming part of the wiki that future queries can draw on.

The compounding effect is what differentiates a living wiki from a growing pile of notes.

## Evidence & Examples

- A book wiki grows richer as each chapter is ingested: character motivations clarified, plot threads cross-linked, themes traced across chapters. [[wiki/sources/llm-wiki-idea]]
- A research wiki can track an evolving thesis: early sources establish a hypothesis, later sources challenge or refine it, contradictions are flagged explicitly. [[wiki/sources/llm-wiki-idea]]

## Connections

- [[wiki/concepts/rag]] — RAG is the non-compounding alternative: no accumulation, no synthesis.
- [[wiki/concepts/zettelkasten]] — the canonical human compounding system: atomic notes linked by meaning, growing richer over time. ZKM is what LLM Wiki automates.
- [[wiki/concepts/building-a-second-brain]] — BASB manages resources but does not compound them into knowledge; contrast with ZKM and LLM Wiki.
- [[wiki/concepts/schema-driven-agents]] — the schema is what gives the LLM the discipline to compound properly (update rather than append, cross-link, flag contradictions).
- [[wiki/entities/vannevar-bush]] — Memex vision anticipated compounding via "associative trails."

## Sources

- [[wiki/sources/llm-wiki-idea]] — central claim of the document.
- [[wiki/sources/building-a-second-brain-and-zettelkasten]] — frames BASB vs. ZKM as non-compounding vs. compounding approaches to knowledge.
