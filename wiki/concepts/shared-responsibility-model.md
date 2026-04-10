---
date: 2026-04-11
type: concept
name: Shared Responsibility Model
aliases: [cloud shared responsibility]
tags: [cloud, backup, resilience, security, governance]
sources: 1
---

# Shared Responsibility Model

## Definition

The cloud-service principle that the provider is responsible for running and securing the platform itself, while the customer remains responsible for the protection, recoverability, and governance of the data and workflows they place inside that platform.

## Detail

In the Microsoft 365 source, this model is used to puncture a common false assumption: if the SaaS product stays available, then the customer's working state must also be recoverable. The article argues that these are different things. A provider can keep the service online while the customer still struggles to rebuild a deleted mailbox, restore a clean file set after sync corruption, or recover the context around a project after an account is removed.

This makes the shared-responsibility model less about abstract cloud architecture and more about operational discipline. Customers need to decide what counts as recoverable, where clean restore points live, and whether recovery procedures have ever been tested under realistic conditions.

## Evidence & Examples

- The source explicitly says Microsoft keeps the platform available while the customer remains responsible for the data inside it [[wiki/sources/do-robotics-firms-need-microsoft-365-backups]]
- Deleted accounts and bad sync events are used as examples where service availability does not guarantee operational recovery [[wiki/sources/do-robotics-firms-need-microsoft-365-backups]]
- The article's backup-vendor comparison is framed as a response to this responsibility gap [[wiki/sources/do-robotics-firms-need-microsoft-365-backups]]

## Connections

- [[wiki/entities/microsoft-365]] — the platform used here to explain the model in practical terms
- [[wiki/concepts/retention-vs-recovery]] — keeping data and restoring working state are different responsibilities
- [[wiki/concepts/restore-testing]] — the model becomes real only when recovery assumptions are exercised
- [[wiki/concepts/ai-cybersecurity]] — incident recovery and integrity protection make the model operationally important, not merely contractual

## Contradictions

- No contradiction captured yet; the current source set does not include Microsoft's own framing or evidence on what native recovery covers well versus poorly.

## Sources

- [[wiki/sources/do-robotics-firms-need-microsoft-365-backups]] — applies the shared-responsibility model to Microsoft 365 backup and recovery in robotics contexts
