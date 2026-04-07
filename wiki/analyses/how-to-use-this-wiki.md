---
type: analysis
title: How to Use This Wiki
date: 2026-04-06
tags: [meta, usage, reference]
---

# How to Use This Wiki

## Operations

| What you want | What to say |
|---|---|
| Add a new source | Drop a file in `raw/sources/`, then say **"ingest filename.md"** |
| Ask a question | Just ask — I'll search the index, read relevant pages, answer with citations |
| Save a good answer | Say **"save this as an analysis page"** |
| Health check | Say **"lint the wiki"** |

## Session Start

Every session, Claude reads:
1. `CLAUDE.md` — schema and all operating rules
2. `wiki/index.md` — full catalog of pages
3. `wiki/log.md` — top entries for recent context

Then greets you with a 1-line status: how many sources, entities, and concepts are indexed.

## Obsidian Tips

- Open the vault folder in Obsidian and use **graph view** to see the shape of the wiki — hubs, orphans, clusters.
- Install **Obsidian Web Clipper** (browser extension) to clip web articles directly to `raw/sources/` as markdown.
- In Settings → Files and links, set attachment folder to `raw/assets/` so images are saved locally.
- **Marp** plugin: generate slide decks from wiki pages.
- **Dataview** plugin: query YAML frontmatter across pages for dynamic tables/lists.

## Key File Locations

| File | Purpose |
|---|---|
| `CLAUDE.md` | Agent schema — defines all conventions and workflows |
| `wiki/index.md` | Master catalog of every wiki page |
| `wiki/log.md` | Chronological history of all operations |
| `wiki/overview.md` | Evolving high-level synthesis |
| `raw/sources/` | Your source files — immutable, never edited by Claude |
| `wiki/sources/` | One summary page per ingested source |
| `wiki/entities/` | People, orgs, products, places |
| `wiki/concepts/` | Ideas, frameworks, methodologies |
| `wiki/analyses/` | Saved query answers and deep-dives |
