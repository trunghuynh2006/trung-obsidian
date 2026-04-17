---
date: 2026-04-18
type: concept
name: Wire Tap
aliases: [wiretap, message tap]
tags: [enterprise-integration, messaging, patterns, monitoring]
sources: 1
---

# Wire Tap

## Definition

A simple component that consumes a message from one channel and republishes it to two channels: the original downstream channel (unmodified) and a secondary channel (e.g., for monitoring or logging).

## Detail

**The problem:** A Point-to-Point Channel delivers each message to exactly one consumer. You cannot simply add a second subscriber to observe messages without intercepting them from the primary consumer. But you want to monitor or store messages without disrupting the main flow.

**The solution:** Insert a Wire Tap between the sender and the primary consumer. The Wire Tap is transparent to both ends — it consumes from the incoming channel and re-publishes the same message to both the primary channel and the secondary (observation) channel.

**Difference from Publish-Subscribe Channel:** On a Pub-Sub channel, you can just add a subscriber. The Wire Tap is specifically for Point-to-Point channels where you cannot add subscribers.

**Non-intrusiveness:** The Wire Tap does not modify the message or delay primary delivery. It simply creates a copy.

**Common secondary uses:**
- Feed a [[wiki/concepts/message-store]] for status tracking.
- Feed a [[wiki/concepts/control-bus]] for metrics collection.
- Feed audit/logging systems.

## Evidence & Examples

- WGRUS: Wire Tap inserted on Point-to-Point channels to copy messages to the Message Store for order status tracking, without disrupting the primary order processing flow [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/message-channel]] — Wire Tap applies specifically to Point-to-Point channels
- [[wiki/concepts/message-store]] — common destination for the secondary channel from a Wire Tap
- [[wiki/concepts/control-bus]] — another common secondary destination for operational metrics
- [[wiki/concepts/smart-proxy]] — more powerful: intercepts and modifies request/reply, vs. Wire Tap's passive copy

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS order status tracking to enable Message Store tapping on Point-to-Point channels
