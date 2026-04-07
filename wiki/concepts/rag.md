---
type: concept
name: RAG (Retrieval-Augmented Generation)
aliases: [RAG, retrieval-augmented generation]
tags: [llm, knowledge-management, architecture]
sources: 1
---

# RAG (Retrieval-Augmented Generation)

## Definition

A pattern where an LLM answers questions by first retrieving relevant chunks from a document collection at query time, then generating an answer from those chunks. The documents themselves are not transformed — they're indexed for retrieval and read on demand.

## Detail

RAG is the dominant approach for LLM + documents today. Products like NotebookLM, ChatGPT file uploads, and most enterprise document Q&A tools use this pattern. The LLM never accumulates knowledge — it rediscovers it from scratch on every query by finding and reading relevant fragments.

**Strengths of RAG:**
- Low setup cost — just index and query.
- Always reads from source — no stale summaries.
- Scales to very large document collections with embedding search.

**Weaknesses of RAG:**
- No accumulation — every query re-derives from scratch.
- Poor at synthesis questions requiring many fragments.
- Contradictions across sources are never resolved — the LLM sees whatever it retrieves.
- No compounding — the 100th query is no better-informed than the 1st.

## Connections

- [[wiki/concepts/knowledge-compounding]] — LLM Wiki exists precisely to address RAG's no-accumulation weakness.
- [[wiki/sources/llm-wiki-idea]] — source that introduces the RAG vs. LLM Wiki contrast.

## Contradictions

*(None yet.)*

## Sources

- [[wiki/sources/llm-wiki-idea]] — frames RAG as the baseline that LLM Wiki improves upon.
