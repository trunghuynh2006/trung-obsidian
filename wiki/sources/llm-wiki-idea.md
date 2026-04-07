---
type: source
title: LLM Wiki — A Pattern for Personal Knowledge Bases
source_file: raw/sources/llm-wiki-idea.md
date_ingested: 2026-04-06
tags: [knowledge-management, llm, second-brain, obsidian, rag]
---

# LLM Wiki — A Pattern for Personal Knowledge Bases

**Source:** [[raw/sources/llm-wiki-idea]]
**Ingested:** 2026-04-06
**Tags:** #knowledge-management #llm #second-brain #obsidian #rag

## Summary

This document introduces the LLM Wiki pattern: instead of using an LLM for retrieval-at-query-time (RAG), you use it to incrementally build and maintain a persistent wiki. When a new source arrives, the LLM reads it, extracts key information, and integrates it into the existing wiki — updating entity pages, revising concept summaries, flagging contradictions. The knowledge is compiled once and kept current, rather than re-derived on every query.

The central insight is that the wiki is a **compounding artifact**. Cross-references, contradictions, and synthesis are baked in. The more sources you add, the richer the wiki becomes — without any manual bookkeeping. The human provides sources and asks good questions; the LLM does all the maintenance.

The architecture has three layers: immutable raw sources, the LLM-maintained wiki, and a schema document (CLAUDE.md) that defines conventions and workflows. The schema is what transforms the LLM from a generic chatbot into a disciplined wiki maintainer.

The pattern is deliberately domain-agnostic and modular — it works for personal notes, research, book reading, business intelligence, or any context where knowledge accumulates over time.

## Key Points

- RAG re-derives knowledge from scratch on every query; LLM Wiki compiles it once and keeps it current.
- The wiki is a persistent, compounding artifact — cross-references and contradictions pre-computed.
- Three layers: raw sources (immutable), wiki (LLM-owned), schema (CLAUDE.md — defines conventions).
- Three operations: **Ingest** (add source → update wiki), **Query** (answer from wiki, optionally save answer), **Lint** (health-check for orphans, contradictions, gaps).
- `index.md` is content-oriented (catalog); `log.md` is chronological (history).
- A single ingest may touch 10–15 wiki pages.
- Good query answers should be filed back into the wiki as analysis pages — explorations compound too.
- Use cases: personal growth, research, book reading, business/team intelligence, hobby deep-dives.
- Tooling: Obsidian (reader/IDE), Web Clipper (sourcing), Marp (slides), Dataview (frontmatter queries), qmd (search at scale).
- Related in spirit to Vannevar Bush's Memex (1945) — the missing piece was who does the maintenance.

## Connections

- [[wiki/concepts/rag]] — LLM Wiki is a deliberate alternative to RAG; understanding the difference is central.
- [[wiki/concepts/knowledge-compounding]] — the core value proposition: accumulated synthesis vs. on-demand retrieval.
- [[wiki/concepts/schema-driven-agents]] — CLAUDE.md / AGENTS.md as the mechanism that makes the LLM disciplined.
- [[wiki/entities/vannevar-bush]] — intellectual ancestor; his Memex vision predates LLMs by 80 years.
- [[wiki/entities/obsidian]] — the recommended reading/browsing tool; "Obsidian is the IDE, the LLM is the programmer."

## Quotes

> "The wiki is a persistent, compounding artifact. The cross-references are already there. The contradictions have already been flagged."

> "LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass. The wiki stays maintained because the cost of maintenance is near zero."

> "Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase."

> "The human's job is to curate sources, direct the analysis, ask good questions, and think about what it all means. The LLM's job is everything else."
