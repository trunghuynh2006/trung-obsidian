---
date: 2026-04-18
type: concept
name: Message Store
aliases: [message database, order store]
tags: [enterprise-integration, messaging, patterns, monitoring]
sources: 1
---

# Message Store

## Definition

A persistent store (typically a database) that saves copies of messages as they flow through the system, enabling status queries, auditing, and process state tracking without disturbing the main message flow.

## Detail

**The status tracking problem:** In an asynchronous messaging system, a business transaction spans multiple messages across multiple systems. There is no single "current state" to query. The Message Store solves this by accumulating all related messages into one queryable location.

**How to tap into message flow:**
- On a **Publish-Subscribe Channel**: add the Message Store as a subscriber. It receives copies of all messages without affecting other subscribers.
- On a **Point-to-Point Channel**: insert a [[wiki/concepts/wire-tap]] that copies each message to a secondary channel feeding the Message Store.

**From Message Store → Process Manager:** When the Message Store is enhanced to not just store messages but also determine the next processing step based on stored state, it becomes a [[wiki/concepts/process-manager]]. The transition: "What is the current status?" → "What should happen next?"

**Shared access pattern (Claim Check):** Once order data is in the Message Store, subsequent messages only need to carry a reference (order ID) rather than the full data. Components retrieve full data from the store when needed — the [[wiki/concepts/claim-check]] pattern.

**Performance note:** For synchronous status queries (e.g., a customer checking order status on the web), accessing the Message Store database directly is the simplest and most efficient approach — no need to send a query message and wait for a reply.

## Evidence & Examples

- WGRUS: a Message Store subscribes to `NEW_ORDER` and `VALIDATED_ORDER` channels; the web interface queries the store database directly to display order status [[wiki/sources/enterprise-integration-patterns-ch1]]
- WGRUS: the Message Store evolves into a Process Manager when it gains the logic to determine whether to trigger shipping/billing based on stored state [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/wire-tap]] — used to copy messages from Point-to-Point channels to the Message Store
- [[wiki/concepts/process-manager]] — a Message Store that also manages process progression
- [[wiki/concepts/claim-check]] — using the Message Store as the "coat check" for large data
- [[wiki/concepts/message-channel]] — the source channels from which the store receives copies

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS order status tracking; transitions to Process Manager design
