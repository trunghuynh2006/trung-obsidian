---
type: entity
name: Obsidian
aliases: []
tags: [product, tool, knowledge-management, markdown]
sources: 1
---

# Obsidian

**Type:** product / software tool
**Category:** Personal knowledge management (PKM)

## Overview

A local-first markdown note-taking application built around bidirectional links and a graph view. Notes are plain `.md` files stored on disk — no proprietary format, no cloud lock-in. Obsidian's core innovation is treating the links between notes as a first-class feature, visualized via its graph view.

In the LLM Wiki pattern, Obsidian plays the role of the **IDE** — the human's reading and browsing interface. The LLM writes and maintains the wiki files; the human reads them in Obsidian, follows links, checks the graph view, and browses the evolving knowledge base in real time.

## Key Facts

- Local-first: all files are plain markdown on your filesystem. [[wiki/sources/llm-wiki-idea]]
- Graph view: visualizes which pages link to which — useful for spotting hubs and orphans.
- **Web Clipper** browser extension: converts web articles to local markdown. [[wiki/sources/llm-wiki-idea]]
- **Marp** plugin: renders markdown as slide decks.
- **Dataview** plugin: runs SQL-like queries over YAML frontmatter across notes.
- Attachment folder setting: auto-saves pasted/downloaded images to a configurable local path.

## Role in LLM Wiki

> "Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase." [[wiki/sources/llm-wiki-idea]]

The recommended workflow: LLM agent open in terminal on one side, Obsidian open on the other. The agent edits files; the user browses results in real time.

## Connections

- [[wiki/concepts/knowledge-compounding]] — graph view reveals the shape of accumulated knowledge.
- [[wiki/entities/vannevar-bush]] — Obsidian's wiki-links are the closest modern analog to Memex associative trails.

## Sources

- [[wiki/sources/llm-wiki-idea]] — recommends Obsidian as the primary reading interface for LLM Wiki.
