---
date: 2026-04-11
type: entity
name: Microsoft PL-400
aliases: [PL-400, Power Platform Developer Associate, Microsoft Power Platform Developer]
tags: [certification, microsoft, power-platform, developer]
sources: 0
---

# Microsoft PL-400

**Type:** product/certification
**Also known as:** PL-400, Power Platform Developer Associate

## Overview

Microsoft PL-400 is the **Power Platform Developer** associate-level certification exam. It targets developers who extend, customize, and integrate the Power Platform — building custom components, plugins, connectors, and automated workflows that go beyond what low-code tools support out of the box.

Unlike the citizen developer certifications (PL-200, PL-100), PL-400 requires genuine software development competence: writing C# plugins that execute inside the Dataverse pipeline, building PCF (Power Apps Component Framework) controls in TypeScript, creating custom connectors via OpenAPI specs, and designing integration architectures that connect Power Platform to external systems.

## Skill Domains

The exam is organized into seven domains (approximate weights):

| Domain | Weight |
|---|---|
| Create technical design | 10–15% |
| Configure Microsoft Dataverse | 15–20% |
| Create and configure Power Apps | 15–20% |
| Configure business process automation | 5–10% |
| Extend the user experience (PCF) | 10–15% |
| Extend the platform (plugins, custom APIs) | 15–20% |
| Develop integrations | 5–10% |

## Key Technical Areas

- **Dataverse**: table design, relationships, security roles, column-level security, business rules, calculated/rollup columns
- **Power Apps**: canvas app formulas, model-driven app customization, responsive design, offline capability
- **Power Automate**: cloud flows, desktop flows (RPA), approvals, exception handling, child flows
- **Plugins**: C# IPlugin interface, execution context, pre/post-images, synchronous vs. asynchronous, sandbox isolation, tracing
- **PCF Controls**: TypeScript component lifecycle, manifest, virtual/standard components, React-based controls
- **Custom Connectors**: OpenAPI definition, authentication flows (OAuth2, API key), triggers vs. actions
- **Azure Integration**: Functions, Service Bus, Logic Apps as integration partners

## Connections

- [[wiki/concepts/ultralearning]] — framework for accelerating exam preparation
- [[wiki/analyses/ultralearning-for-pl400]] — full study plan applying ultralearning to this exam
- [[wiki/entities/microsoft-365]] — Microsoft ecosystem this platform extends

## Open Questions

- Which PCF control scenarios are currently most tested (virtual vs. standard vs. React)?
- How heavily does the exam test Power Pages vs. Power Apps?
- Are there significant gaps between the official study guide and actual exam emphasis?
