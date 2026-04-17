---
date: 2026-04-18
type: concept
name: File Transfer
aliases: [file-based integration, batch file integration]
tags: [enterprise-integration, integration-styles, patterns]
sources: 1
---

# File Transfer

## Definition

An integration style where applications share data by producing and consuming files. Each application writes shared data to files at regular intervals; other applications read those files when they need the data.

## Detail

**How it works:** Each application produces files containing the information other applications need. Integrators handle format transformation between files. Files are produced on a regular business cycle (nightly, weekly, quarterly).

**Why it fits many situations:** Files are universal — every OS, every language can read and write them. No specialized middleware is required. The producer and consumer are completely independent: the producer writes when ready; the consumer reads when ready; neither is aware of the other's internals.

**Seven-criteria assessment:**

| Criterion | Rating | Notes |
|-----------|--------|-------|
| Coupling | ✅ Low | Each app's file format is its only external interface |
| Simplicity | ✅ High | No extra infrastructure; the app team usually provides the file |
| Integration technology | ✅ None needed | Works with what the enterprise already has (FTP, shared disk) |
| Data format | ⚠️ Requires negotiation | Formats must be agreed; transformations are manual |
| Timeliness | ❌ Low | Nightly/weekly cycles; data can be stale for hours or days |
| Data-vs-functionality | ❌ Data only | Cannot invoke behavior in the other system |
| Asynchronicity | ✅ Fully async | No temporal coupling; writer and reader run independently |

**The staleness problem:** If a customer changes address and the extract runs nightly, the billing system may send a bill to the old address the same day. Staleness also creates inconsistency: two systems updated independently can produce conflicting records.

**The infrastructure you still need yourself:**
- File naming conventions and directories
- Unique filename strategy (writer must ensure no collisions)
- Locking: prevent reader from starting while writer is still writing
- File transfer if apps don't share a disk
- Cleanup: deciding when old files are no longer needed

**Relationship to Messaging:** File Transfer taken to its logical extreme — one file per change, produced immediately — becomes Messaging. At that granularity, the file management overhead becomes prohibitive and you need messaging infrastructure.

## When to use

- Bulk data updates (full catalog refresh, end-of-day batch reports)
- Low update frequency (quarterly supplier catalog updates)
- Simple format, low semantic complexity
- When neither app can be changed to support a richer interface

**WGRUS example:** Supplier catalog updates: suppliers update catalogs quarterly, so File Transfer (FTP) is more appropriate than a real-time messaging infrastructure. [[wiki/sources/enterprise-integration-patterns-ch1]]

## Contradictions

None yet.

## Connections

- [[wiki/concepts/shared-database]] — next step up: timely but couples via schema
- [[wiki/concepts/remote-procedure-invocation]] — if you need to share functionality, not just data
- [[wiki/concepts/messaging-integration]] — the evolution of File Transfer when fine-grained timeliness is needed
- [[wiki/concepts/enterprise-application-integration]] — one of four integration styles

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch2]] — full pattern treatment: forces, solution, consequences; written by Martin Fowler
- [[wiki/sources/enterprise-integration-patterns-ch1]] — mentioned as the appropriate style for WGRUS quarterly catalog updates
