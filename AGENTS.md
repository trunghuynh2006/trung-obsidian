# LLM Wiki — Agent Schema

This file defines how I (Codex) operate as the wiki maintenance agent for this vault.
Every session starts by reading this file. Every operation follows the rules here.

---

## Directory Layout

```text
/                          ← vault root (this is the working directory)
├── AGENTS.md              ← this file — agent schema and rules
├── CLAUDE.md              ← Claude-specific version of the agent schema
├── wiki/                  ← LLM-owned knowledge base
│   ├── index.md           ← master catalog of all wiki pages
│   ├── log.md             ← append-only chronological log
│   ├── overview.md        ← high-level synthesis of the whole wiki
│   ├── sources/           ← one summary page per ingested source
│   ├── entities/          ← people, organizations, products, places
│   ├── concepts/          ← ideas, frameworks, methodologies, terms
│   └── analyses/          ← comparisons, deep-dives, answers saved as pages
└── raw/                   ← user-owned source material (READ ONLY — never modify)
    ├── sources/           ← raw source files: .md, .pdf, .txt, .html, etc.
    └── assets/            ← images and attachments downloaded from articles
```

---

## Page Formats

### Source Summary Page (`wiki/sources/<slug>.md`)
```markdown
---
type: source
title: <full title>
source_file: raw/sources/<filename>
date_ingested: YYYY-MM-DD
tags: [<tag1>, <tag2>]
---

# <Title>

**Source:** [[raw/sources/<filename>]]
**Ingested:** YYYY-MM-DD
**Tags:** #tag1 #tag2

## Summary
2–4 paragraph synthesis of the key content.

## Key Points
- Bullet list of the most important claims, facts, or ideas.

## Connections
Links to entity and concept pages this source touches, with one-line notes.
- [[wiki/entities/foo]] — source supports X claim about foo
- [[wiki/concepts/bar]] — source introduces bar framework

## Quotes
Notable verbatim excerpts worth preserving.
```

### Entity Page (`wiki/entities/<slug>.md`)
```markdown
---
type: entity
name: <canonical name>
aliases: [<alt name>, ...]
tags: [<tag>]
sources: <count>
---

# <Name>

**Type:** person | org | product | place | event
**Also known as:** alias1, alias2

## Overview
1–3 paragraph description synthesized from all sources.

## Key Facts
- Fact 1 [[source]]
- Fact 2 [[source]]

## Timeline
- YYYY: event [[source]]

## Connections
- [[wiki/entities/other]] — relationship
- [[wiki/concepts/idea]] — how this entity relates

## Open Questions
- Things still unknown or contradicted across sources.

## Sources
- [[wiki/sources/slug]] — what this source adds
```

### Concept Page (`wiki/concepts/<slug>.md`)
```markdown
---
type: concept
name: <canonical name>
aliases: []
tags: []
sources: <count>
---

# <Concept Name>

## Definition
Concise definition synthesized from all sources.

## Detail
Deeper explanation, nuance, variants.

## Evidence & Examples
- Example 1 [[source]]
- Counterexample 1 [[source]]

## Connections
- [[wiki/concepts/related]] — relationship
- [[wiki/entities/entity]] — entities that embody or use this concept

## Contradictions
Note any claims across sources that conflict, with citations.

## Sources
- [[wiki/sources/slug]] — what this source adds
```

### Analysis Page (`wiki/analyses/<slug>.md`)
```markdown
---
type: analysis
title: <title>
date: YYYY-MM-DD
tags: []
---

# <Title>

**Date:** YYYY-MM-DD
**Question/Prompt:** <what triggered this analysis>

## Answer / Findings
Main content.

## Sources Consulted
- [[wiki/sources/slug]]

## Follow-up Questions
```

---

## Operations

### INGEST — Adding a new source

**Trigger:** User drops a file in `raw/sources/` and says "ingest <filename>" (or similar).

**Steps (in order):**
1. Read the source file fully.
2. Discuss key takeaways with the user — ask what angle they care about most.
3. Create `wiki/sources/<slug>.md` with the source summary page.
4. Identify entities mentioned → create or update their pages in `wiki/entities/`.
5. Identify concepts introduced or referenced → create or update `wiki/concepts/` pages.
6. Update `wiki/index.md` — add the new source page and any new entity/concept pages.
7. Update `wiki/overview.md` to reflect how this source changes or reinforces the big picture.
8. Append to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <Title>`
9. Commit and push: `git add -A && git commit -m "ingest: <Title>" && git push origin master`
10. Report to user: pages created, pages updated, notable connections found.

**Rules:**
- Read every page you're about to update *before* editing it.
- Preserve existing content — integrate, don't overwrite.
- Flag contradictions explicitly: use `> **Contradiction:** ...` callout blocks.
- Cross-link liberally. Every entity and concept page should link back to sources.
- Use `<slug>` = lowercase, hyphens, no special chars (e.g. "John Smith" → `john-smith`).

### QUERY — Answering questions

**Trigger:** User asks a question.

**Steps:**
1. Read `wiki/index.md` to find relevant pages.
2. Read those pages.
3. Synthesize an answer with inline citations to wiki pages.
4. Ask: "Should I save this as an analysis page?" — if yes, create `wiki/analyses/<slug>.md`.
5. If saved, update `wiki/index.md` and append to `wiki/log.md`.

### LINT — Health check

**Trigger:** User says "lint the wiki" or "health check".

**Steps:**
1. Read all pages listed in `wiki/index.md`.
2. Report:
   - Contradictions between pages
   - Orphan pages (no inbound links from other wiki pages)
   - Mentioned concepts/entities that lack their own page
   - Stale claims that newer sources supersede
   - Missing cross-references that should exist
3. For each issue, propose a fix. Ask user before mass-editing.
4. Append to `wiki/log.md`: `## [YYYY-MM-DD] lint | <summary of issues found>`

---

## Index Format

`wiki/index.md` is organized by category. Each entry: `- [[path/to/page]] — one-line description`.

Sections:
- `## Sources` — ingested source summaries
- `## Entities` — people, orgs, products, places
- `## Concepts` — ideas, frameworks, terms
- `## Analyses` — saved query responses and deep-dives
- `## Meta` — overview, log (always listed)

**Rule:** Update `wiki/index.md` on every ingest and every time a new page is created or significantly changed.

---

## Log Format

`wiki/log.md` is append-only. New entries go at the **top** (most recent first).

Entry format:
```text
## [YYYY-MM-DD] <operation> | <title or description>
<1–3 line summary of what happened, pages touched, notable findings>
```

Operations: `ingest`, `query`, `lint`, `update`, `init`

---

## Conventions

- All wiki pages use `[[wiki-link]]` style for internal links (Obsidian-compatible).
- Slugs: lowercase, hyphens, no spaces or special characters.
- Dates: ISO 8601 (`YYYY-MM-DD`).
