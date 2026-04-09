---
date: 2026-04-07
type: concept
name: Schema-Driven Agents
aliases: [agent schema, CLAUDE.md, AGENTS.md]
tags: [llm, agents, knowledge-management, configuration]
sources: 1
---

# Schema-Driven Agents

## Definition

The pattern of giving an LLM agent a structured configuration document (e.g. CLAUDE.md, AGENTS.md) that defines its domain, conventions, and exact workflows — transforming a generic LLM into a disciplined, domain-specific collaborator.

## Detail

Without a schema, an LLM is a general-purpose assistant that may be helpful but has no consistent behavior across sessions. With a schema document read at session start, the LLM knows:
- What directory structure to expect and maintain.
- What page formats to use for different content types.
- Exactly what steps to follow for each operation (ingest, query, lint).
- What conventions govern naming, linking, and tagging.
- The history of what's been done (via the log).

The schema is co-evolved by the user and the LLM over time. Early sessions establish basic structure; later sessions refine conventions based on what's working. This is the file that makes the LLM a wiki maintainer rather than a chatbot.

**Key design principle:** The schema should be specific enough that any LLM session following it produces consistent results, but not so rigid that it can't adapt to new content types or user needs.

## Connections

- [[wiki/concepts/knowledge-compounding]] — the schema is what gives the agent the discipline to compound properly.
- [[wiki/sources/llm-wiki-idea]] — source that defines this concept in the context of LLM Wiki.

## Sources

- [[wiki/sources/llm-wiki-idea]] — introduces CLAUDE.md / AGENTS.md as the key configuration layer.
