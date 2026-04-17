---
date: 2026-04-18
type: concept
name: Aggregator
aliases: [message aggregator]
tags: [enterprise-integration, messaging, patterns, routing]
sources: 1
---

# Aggregator

## Definition

A component that receives multiple related incoming messages and combines them into a single outgoing message.

## Detail

**UML equivalent:** the join bar in an activity diagram — waits for all parallel branches to complete before proceeding.

**Three design decisions every Aggregator must answer:**

| Decision | Question | WGRUS Example |
|----------|----------|---------------|
| **Correlation** | Which messages belong together? | Order ID (not customer ID — a customer may place multiple orders) |
| **Completeness condition** | When do we have all messages? | Item count from original order; wait for N item results |
| **Aggregation algorithm** | How do we combine them? | Concatenate all item results back into a single order message |

**Correlation caveat:** You cannot correlate on unstable identifiers. WGRUS cannot correlate by customer ID because a customer may place two orders in quick succession, producing interleaved messages. A unique order ID must be assigned before splitting — see [[wiki/concepts/content-enricher]].

**Stateful by nature:** The Aggregator must hold partial results in memory (or persistent store) until all expected messages arrive. This state is the source of the Aggregator's complexity and failure modes (what if one message is lost?).

**Timeout strategy:** A well-designed Aggregator handles the case where not all messages arrive — timeout and route to error handling.

## Evidence & Examples

- WGRUS order validation: Aggregator waits for both the inventory check result and the credit standing result before passing the combined message to the Content-Based Router [[wiki/sources/enterprise-integration-patterns-ch1]]
- WGRUS multi-item orders: Aggregator recombines individual `OrderItem` results into a single `Order` result; completeness = item count from original order [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/splitter]] — the counterpart that breaks one message into many
- [[wiki/concepts/composed-message-processor]] — named composite pattern: Splitter + Router + Aggregator
- [[wiki/concepts/content-enricher]] — adds the correlation ID that the Aggregator uses to group messages
- [[wiki/concepts/process-manager]] — alternative to Aggregator for complex multi-step orchestration; manages state more explicitly

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — used twice in WGRUS: order validation join and multi-item order recombination
