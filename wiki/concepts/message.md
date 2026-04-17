---
date: 2026-04-18
type: concept
name: Message
aliases: [Document Message, Command Message, Event Message]
tags: [enterprise-integration, messaging, patterns]
sources: 1
---

# Message

## Definition

A self-contained, atomic packet of data sent between two applications via a Message Channel. The message defines both a payload and an agreed-upon meaning — both sender and receiver must understand what it represents.

## Detail

A message is the fundamental unit of communication in a messaging-based integration solution. It can be very small (a single changed phone number) or very large (a complete customer list). The key property is that the channel knows how much data constitutes one message, enabling queuing and routing.

**Three message subtypes** (Hohpe & Woolf):

| Subtype | Intent | Example |
|---------|--------|---------|
| **Document Message** | Pass a document; receiver decides what to do | `NEW_ORDER` — passes order data; receivers (inventory, billing, shipping) each act on it as they see fit |
| **Command Message** | Instruct receiver to execute a specific action | `CHECK_INVENTORY` — tells the inventory system to verify item availability |
| **Event Message** | Notify that something happened; receivers react if interested | `ADDRESS_CHANGED` — notifies all interested parties |

**Channel naming convention** (from WGRUS):
- Canonical (public) channels: named after the message intent — `NEW_ORDER`, `VALIDATED_ORDER`
- Application-specific (private) channels: prefixed with the app name — `WEB_NEW_ORDER`, `FAX_NEW_ORDER`
- Meaning shifts with the channel: the same message type on `NEW_ORDER` vs `INVALID_ORDER` carries entirely different business meaning.

## Evidence & Examples

- WGRUS `NEW_ORDER` channel: uses Document Message — intent is to pass order data, not dictate what each system does [[wiki/sources/enterprise-integration-patterns-ch1]]
- WGRUS inventory routing: uses Command Message — `CHECK_INVENTORY` tells the inventory system what to do [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/message-channel]] — the conduit through which messages travel
- [[wiki/concepts/message-translator]] — converts message format between sender and receiver schemas
- [[wiki/concepts/canonical-data-model]] — defines the shared format for canonical messages
- [[wiki/concepts/splitter]] — breaks one message into many
- [[wiki/concepts/aggregator]] — combines many messages into one

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduces message as base concept; Document/Command distinction; channel naming conventions
