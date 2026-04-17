---
date: 2026-04-18
type: concept
name: Shared Database
aliases: [integration database, shared schema]
tags: [enterprise-integration, integration-styles, patterns]
sources: 1
---

# Shared Database

## Definition

An integration style where multiple applications store and access their shared data in a single common database, so any application always sees up-to-date data written by any other.

## Detail

**How it works:** All integrated applications read and write to a single, unified database schema. Any change made by one application is immediately visible to all others via standard SQL reads. Transaction management handles simultaneous updates.

**Seven-criteria assessment:**

| Criterion | Rating | Notes |
|-----------|--------|-------|
| Coupling | ❌ High | Every app is coupled to the shared schema; any schema change ripples everywhere |
| Simplicity | ⚠️ Medium | SQL is universal, but designing a unified schema is very hard |
| Integration technology | ✅ Low overhead | Most apps already use SQL; no extra middleware |
| Data format | ✅ Forces agreement | Apps must agree on schema; resolves semantic dissonance (or forces the fight early) |
| Timeliness | ✅ Immediate | Any write is visible to all readers instantly |
| Data-vs-functionality | ❌ Data only | Cannot invoke behavior; see Remote Procedure Invocation |
| Asynchronicity | ❌ Synchronous | Reads are synchronous; locking contention is a real risk |

**The schema coupling problem:** The unified schema is the integration contract. If any app needs to change how it stores data, the shared schema must change — which requires coordinating every other app that uses that schema. This makes the database a change bottleneck and discourages evolution.

**The political problem:** Agreeing on a single schema requires cross-team, cross-department negotiation about whose data model wins. "Whose notion of 'account' do we use?" This is often a multi-month process even for small schemas.

**The package problem:** Packaged applications (SAP, Oracle, Salesforce) have their own schemas and often cannot adapt to a shared schema. Post-merger integrations face the same wall: acquired companies already have established schemas.

**The performance problem:** Multiple apps reading and writing the same tables simultaneously cause locking conflicts. Distributed databases add latency and consistency complexity. At scale, a Shared Database can become a performance bottleneck and a single point of failure.

**One genuine advantage:** Shared Database forces semantic dissonance to be resolved before the software goes live. File Transfer and Messaging can defer semantic problems; they surface as inconsistencies in production data later. Shared Database makes them unavoidable upfront — which is painful but can be beneficial.

## When to use

- Small number of tightly-related applications that must share the same data model
- Greenfield development where you control all apps
- Reporting databases or data warehouses (read-heavy, no conflict)
- As a Claim Check store alongside a Messaging architecture (read separately from the integration bus)

## Contradictions

None yet.

## Connections

- [[wiki/concepts/file-transfer]] — less timely alternative; avoids schema coupling
- [[wiki/concepts/remote-procedure-invocation]] — add encapsulation on top of shared data
- [[wiki/concepts/messaging-integration]] — alternative that avoids schema coupling while maintaining timeliness
- [[wiki/concepts/canonical-data-model]] — in Messaging, the CDM plays a similar semantic-agreement role without schema coupling
- [[wiki/concepts/enterprise-application-integration]] — one of four integration styles

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch2]] — full pattern treatment: forces, solution, consequences
