---
date: 2026-04-18
type: concept
name: Process Manager
aliases: [orchestrator, saga orchestrator]
tags: [enterprise-integration, messaging, patterns, orchestration]
sources: 1
---

# Process Manager

## Definition

A central component that manages the execution of a multi-step business process across multiple systems by storing intermediate state and determining the next processing step based on that state.

## Detail

**Two core functions:**
1. **Storing data between messages** — holds context (e.g., order details, results received so far) in a persistent store so intermediate messages don't have to carry all data.
2. **Tracking progress and determining the next step** — inspects stored state to decide what action to trigger next (e.g., "both inventory and credit checks are done → trigger shipping and billing").

**How it differs from Aggregator:** An Aggregator knows in advance how to combine messages (fixed algorithm, fixed completeness condition). A Process Manager handles more complex, conditional flows where the next step depends on accumulated state. The Process Manager is the general case; the Aggregator is the specific, stateless case.

**Evolution path (WGRUS):** Message Store (passive log) → Process Manager (active orchestrator). When the store gains the logic to *determine what should happen next* based on stored state, it becomes a Process Manager.

**Service-enabling effect:** A Process Manager exposes individual downstream systems as Shared Services — each system responds to commands without knowing the overall business process. This increases reuse and simplifies each system's logic.

**Persistent store:** Typically a relational database or file system. Each process instance is a row/record identified by a correlation ID.

**Return Address coupling:** Services exposed by a Process Manager need to support [[wiki/concepts/return-address]] — the caller specifies where to send the reply. A Process Manager generates unique reply channels per process instance.

## Evidence & Examples

- WGRUS order status + SOA design: the Message Store evolves into a Process Manager that determines whether to trigger billing and shipping based on stored inventory + credit results [[wiki/sources/enterprise-integration-patterns-ch1]]
- WGRUS address change: a lightweight Process Manager sequences two messages to the billing system (first update address, then send bill) to ensure correct ordering [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/aggregator]] — simpler alternative for fixed-formula result combination
- [[wiki/concepts/message-store]] — a Message Store that gains routing logic becomes a Process Manager
- [[wiki/concepts/return-address]] — services invoked by a Process Manager must support Return Address
- [[wiki/concepts/smart-proxy]] — wraps legacy services to make them compatible with Return Address / Process Manager patterns
- [[wiki/concepts/composed-message-processor]] — a fixed-pattern composite; Process Manager is the general flexible alternative

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced as the evolution of the Message Store in WGRUS; used in address-change sequencing
