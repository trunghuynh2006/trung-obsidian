---
date: 2026-04-18
type: concept
name: Content-Based Router
aliases: [CBR, message router]
tags: [enterprise-integration, messaging, patterns, routing]
sources: 1
---

# Content-Based Router

## Definition

A routing component that consumes an incoming message and republishes it (unmodified) to one of several output channels based on rules applied to the message's content.

## Detail

The Content-Based Router is the fundamental conditional routing pattern. It inspects the message payload or headers and selects the appropriate downstream channel. The message itself is not transformed — routing is the only operation.

**Equivalent in UML:** the branch/decision node in an activity diagram.

**Key design consideration:** what happens to messages that match no routing rule? They should be routed to an [[wiki/concepts/message-channel#Invalid Message Channel]] rather than silently dropped.

**Avoiding hidden coupling:** Without a CBR, the sending application must know the addresses of all downstream systems — creating location and logic coupling. The CBR centralizes that routing logic; adding a new downstream system only requires updating the router, not the sender.

## Evidence & Examples

- WGRUS inventory routing: orders with item numbers starting 'W' → widget inventory; starting 'G' → gadget inventory; neither → `INVALID_ORDER` [[wiki/sources/enterprise-integration-patterns-ch1]]
- WGRUS order validation: after Aggregator combines inventory + credit results, a CBR routes to `VALIDATED_ORDER` or `INVALID_ORDER` based on outcome [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/message-filter]] — simpler case: passes or drops a message; no multiple output channels
- [[wiki/concepts/recipient-list]] — routes to multiple destinations simultaneously (vs. CBR's exclusive routing)
- [[wiki/concepts/splitter]] — often combined: split a multi-item message, then route each item via CBR
- [[wiki/concepts/composed-message-processor]] — Splitter + CBR + Aggregator as a named composite
- [[wiki/concepts/aggregator]] — the join counterpart to CBR's fork/branch behavior

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — used twice in WGRUS: inventory routing and order validation branching
