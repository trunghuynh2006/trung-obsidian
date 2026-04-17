---
date: 2026-04-18
type: concept
name: Message Channel
aliases: [Point-to-Point Channel, Publish-Subscribe Channel, Datatype Channel, Invalid Message Channel, channel]
tags: [enterprise-integration, messaging, patterns]
sources: 1
---

# Message Channel

## Definition

A logical address — agreed upon by sender and receiver — through which messages flow. Neither party needs to know the other's physical location, technology, or current availability.

## Detail

A channel decouples sender from receiver on location and time: the sender writes to the channel; the channel holds the message until the receiver is ready. The channel is the fundamental loose-coupling mechanism for location and temporal dependencies.

**Four channel variants:**

### Point-to-Point Channel
Each message is delivered to exactly one consumer. Used when only one system should process each message (e.g., an order should be fulfilled only once).
- WGRUS: `NEW_ORDER` is Point-to-Point — each order consumed once by the order processor.

### Publish-Subscribe Channel
Each message is delivered to **all** active subscribers. Used to fan out data or events to multiple interested parties simultaneously.
- WGRUS: `VALIDATED_ORDER` uses Pub-Sub to simultaneously trigger shipping and billing.
- Advantage: new subscribers can be added without changing the publisher.
- Limitation: less control over who receives messages; works best on local networks.

### Datatype Channel
A channel that carries messages of a single type only. Consumers know exactly what message format to expect without inspecting each message.
- WGRUS: `NEW_ORDER` is a Datatype Channel — always contains new order messages.

### Invalid Message Channel
A channel where messages are routed when they cannot be processed (wrong format, unrecognized item type, validation failure). Separates error handling from the main flow.
- WGRUS: orders with item numbers that start with neither 'W' nor 'G' are routed to `INVALID_ORDER`.
- The same message type means something entirely different depending on which channel it appears on.

## Evidence & Examples

- Adding a Pub-Sub subscriber to track order status in a Message Store without disturbing message flow [[wiki/sources/enterprise-integration-patterns-ch1]]
- Wire Tap used to copy messages from a Point-to-Point Channel to a second channel (since P2P can't have multiple subscribers directly) [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/message]] — the payload that travels through channels
- [[wiki/concepts/message-endpoint]] — connects an application to a channel
- [[wiki/concepts/wire-tap]] — copies a message from one channel to two
- [[wiki/concepts/recipient-list]] — explicitly addresses a set of channels
- [[wiki/concepts/content-based-router]] — routes messages to different channels based on content

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — defines channel types; WGRUS uses all four variants
