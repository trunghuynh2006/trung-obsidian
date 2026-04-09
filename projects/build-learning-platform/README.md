---
date: 2026-04-09
type: project
title: Build Learning Platform
status: active
tags: [edtech, ai, knowledge-graph, full-stack]
---

# Build Learning Platform

**Status:** active
**Started:** 2026-04-09
**Last Updated:** 2026-04-09

## Goal
Create a collaborative platform for learning programming — connecting learners, teachers, and admins through structured content (knowledge graph), an AI tutor, and role-specific workflows.

## Current Focus
- Designing the knowledge graph schema (Topic / Concept / LearningUnit hierarchy)
- Defining the AI tutor panel UX and interaction model
- Writing the PRD covering learner, teacher, and admin roles

## Next Actions
- [ ] Define Topic / Concept / LearningUnit schema — relationships, cardinality, storage format
- [ ] Decide between FastAPI (Python) and Go for the backend — benchmark priorities: dev speed vs. concurrency
- [ ] Research payment / subscription system options (Stripe, Paddle, etc.)

## Stack / Decisions
- Backend: TBD — FastAPI vs. Go (decision pending)
- Payment: TBD — researching Stripe / Paddle
- Data model: knowledge graph (schema in progress)

## Wiki Connections
- [[wiki/concepts/knowledge-graph]] — if/when ingested: relevant to Topic/Concept/LearningUnit schema design
- [[wiki/concepts/ai-tutor]] — AI tutor panel design may draw on LLM interaction patterns in wiki

## Log
[[projects/build-learning-platform/log]]
