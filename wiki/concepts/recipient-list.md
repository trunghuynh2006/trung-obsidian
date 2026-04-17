---
date: 2026-04-18
type: concept
name: Recipient List
aliases: [Dynamic Recipient List, Dynamic Router, dynamic recipient list]
tags: [enterprise-integration, messaging, patterns, routing]
sources: 1
---

# Recipient List

## Definition

A router that sends a copy of each incoming message to an explicit, enumerated list of output channels — giving the sender precise control over which recipients receive the message.

## Detail

**Difference from Publish-Subscribe Channel:** A Pub-Sub channel sends to all active subscribers and cannot easily control who subscribes. A Recipient List explicitly addresses each recipient, so the publisher knows and controls exactly who receives each message.

**Why it matters:** Pub-Sub is unsuitable when:
- Recipients should not all see every message (e.g., preferred-customer offers should not reach regular customers).
- Recipients are geographically dispersed (Pub-Sub over WAN generates redundant traffic for uninterested parties).

### Dynamic Recipient List

A Recipient List whose recipient set changes based on control messages (subscriptions). The combination of:
- **Recipient List** — addresses recipients explicitly (vs. Pub-Sub's broadcast)
- **Dynamic Router** — routing rules can be updated via control messages (e.g., subscription requests from subscribers)

Together: subscribers register preferences; the Dynamic Recipient List keeps a subscriber registry and routes each announcement only to interested, authorized subscribers.

**Implementation note:** When recipients communicate via email, the Dynamic Recipient List is essentially a mailing list. When recipients use SOAP/Web services, the channel address is a URI. The pattern is transport-independent.

## Evidence & Examples

- WGRUS announcements: marketing sends promotional messages to customers. Customers subscribe with preferences (widget deals, gadget deals, preferred-customer only). A Dynamic Recipient List routes each announcement only to interested, authorized recipients [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/message-channel]] — Pub-Sub Channel is the alternative with less control
- [[wiki/concepts/message-filter]] — simpler alternative when filtering can happen at the receiver side
- [[wiki/concepts/content-based-router]] — routes to exclusive channels; Recipient List routes to multiple simultaneously

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — Dynamic Recipient List introduced for WGRUS customer announcements
