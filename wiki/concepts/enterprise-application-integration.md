---
date: 2026-04-18
type: concept
name: Enterprise Application Integration
aliases: [EAI, application integration]
tags: [enterprise-integration, software-architecture]
sources: 2
---

# Enterprise Application Integration (EAI)

## Definition

The discipline of connecting multiple applications within (or across) an enterprise so they can share data and coordinate business processes, despite differences in platform, language, location, and data format.

## Detail

Enterprises accumulate applications organically: best-of-breed selection, mergers, legacy systems, departmental tools. A single business transaction (e.g., "place order") typically spans 5–7 systems. Users do not think about system boundaries; the integration must hide them.

**Why integration is hard:**
- **Political**: each app is owned by a business unit; integration requires cross-unit coordination.
- **Control**: integration developers rarely control the apps they connect — they are usually packaged or legacy systems.
- **Standards fragmentation**: XML solves syntax, not semantics. Two systems using XML still disagree on what "account" means.
- **Operational complexity**: distributed solutions are hard to deploy, monitor, and debug.

**Seven integration decision criteria** (Ch2):

| Criterion | Question to ask |
|-----------|----------------|
| **Coupling** | How much do the apps need to know about each other's internals? |
| **Integration simplicity** | How much new code and tooling does this require? |
| **Integration technology** | What specialized infrastructure is needed, and at what cost? |
| **Data format** | How do apps agree on data formats, and how do format changes propagate? |
| **Data timeliness** | How quickly must a change in one app be visible to others? |
| **Data vs. functionality** | Do you need to share data, invoke behavior in the other app, or both? |
| **Asynchronicity** | Can the sender proceed without waiting for the receiver to respond? |

**Four integration styles** (Ch2 formal pattern treatment):

| Style | Timeliness | Coupling | Functionality | Async |
|-------|-----------|----------|---------------|-------|
| [[wiki/concepts/file-transfer]] | ❌ Low | ✅ Low | ❌ Data only | ✅ Yes |
| [[wiki/concepts/shared-database]] | ✅ Immediate | ❌ High (schema) | ❌ Data only | ❌ Synchronous |
| [[wiki/concepts/remote-procedure-invocation]] | ✅ Immediate | ⚠️ Medium | ✅ Both | ❌ Synchronous |
| [[wiki/concepts/messaging-integration]] | ✅ High | ✅ Very low | ✅ Both | ✅ Yes |

**Six integration scenario types** (what you're integrating — from Ch1):

| Type | Description | When it fits |
|------|-------------|--------------|
| **Information Portal** | Aggregate data from multiple sources into a single view | Users need read-only access to multi-system data |
| **Data Replication** | Propagate copies of shared reference data across systems | Each system needs local copies; read-heavy; changes are infrequent |
| **Shared Business Function** | Expose a function (e.g., address lookup, tax calc) once, call it from many | Function is expensive to duplicate; low call frequency |
| **Service-Oriented Architecture** | Directory + negotiation + shared services bus | Many services; need discovery + consistent interface contracts |
| **Distributed Business Process** | Orchestrate a multi-step process across existing systems | No single system owns the full workflow |
| **B2B Integration** | Extend integration across enterprise boundaries | External partners, Internet transport, standardized formats critical |

**The middleware stack** (what sits between apps):
1. **Message** — self-contained data packet both sides agree on
2. **Channel** — logical address for sending/receiving messages
3. **Translation** — converts one app's format to another's
4. **Routing** — directs messages to the right destination
5. **Systems Management** — monitoring, error detection, metrics
6. **Endpoint** — connects an app to the messaging infrastructure

## Evidence & Examples

- WGRUS retailer: a single "place order" function spans call center, web, fax, inventory (×2), billing, and shipping systems [[wiki/sources/enterprise-integration-patterns-ch1]]
- ERP systems (SAP, Oracle, PeopleSoft) are among the most common integration points despite being the largest apps — proving no single app can own all business functions [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/loose-coupling]] — the governing design principle
- [[wiki/concepts/message-channel]] — the core infrastructure primitive
- [[wiki/concepts/canonical-data-model]] — the standard answer to the "many translators" problem
- [[wiki/concepts/process-manager]] — the pattern for orchestrating distributed business processes
- [[wiki/entities/gregor-hohpe]] — primary author of the canonical EAI pattern catalog
- [[wiki/entities/bobby-woolf]] — co-author

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — foundational: defines EAI problem space, six integration types, middleware stack, and WGRUS worked example
- [[wiki/sources/enterprise-integration-patterns-ch2]] — adds seven integration criteria and full pattern treatment of the four integration styles
