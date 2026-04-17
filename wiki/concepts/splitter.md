---
date: 2026-04-18
type: concept
name: Splitter
aliases: [message splitter]
tags: [enterprise-integration, messaging, patterns, routing]
sources: 1
---

# Splitter

## Definition

A component that receives one composite message and breaks it into multiple individual messages, each published to the output channel separately.

## Detail

Use a Splitter when a message contains multiple independent items that each need to be routed, processed, or validated separately.

**Why split?** An order with multiple items cannot be routed to a single inventory system — different items belong to different systems (widgets vs. gadgets). Splitting allows each item to be routed, processed, and validated independently.

**The correlation problem:** After splitting, you need to know which item messages belong to the same original message. The split messages must carry a correlation identifier (typically an order ID). See [[wiki/concepts/content-enricher]] — often inserted before the Splitter to add a unique ID.

**Pairing with Aggregator:** A Splitter almost always has a paired [[wiki/concepts/aggregator]] downstream to recombine the processed items back into a single result. The Splitter+CBR+Aggregator combination is so common it has its own pattern name: [[wiki/concepts/composed-message-processor]].

## Evidence & Examples

- WGRUS multi-item order processing: a Splitter breaks an `Order` message into individual `OrderItem` messages. Each `OrderItem` is routed by a Content-Based Router to the correct inventory system [[wiki/sources/enterprise-integration-patterns-ch1]]
- The Aggregator downstream uses the order item count from the original order message as the completeness condition [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/aggregator]] — the join counterpart; recombines split messages
- [[wiki/concepts/composed-message-processor]] — Splitter + Content-Based Router + Aggregator as a named composite
- [[wiki/concepts/content-enricher]] — add a correlation ID before splitting so the Aggregator can group results
- [[wiki/concepts/content-based-router]] — typically used after splitting to route each part

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS multi-item order processing
