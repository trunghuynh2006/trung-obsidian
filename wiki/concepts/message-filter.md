---
date: 2026-04-18
type: concept
name: Message Filter
aliases: [filter]
tags: [enterprise-integration, messaging, patterns, routing]
sources: 1
---

# Message Filter

## Definition

A component that passes messages matching a specified criterion to the output channel and silently drops all others.

## Detail

The Message Filter is a degenerate router: one output channel (pass) and one implicit output (drop). Use it when a subscriber only cares about a subset of messages on a channel.

**Typical use case:** A Publish-Subscribe Channel broadcasts messages to all subscribers. Individual subscribers insert a filter upstream so they only act on relevant messages.

**Difference from Content-Based Router:**
- CBR: one input → one of N output channels (exclusive selection).
- Filter: one input → either the output channel or nothing (pass/drop).

**Difference from Invalid Message Channel routing:** A filter intentionally ignores irrelevant messages (by design, not by error); an Invalid Message Channel receives messages that are malformed or cannot be processed.

## Evidence & Examples

- WGRUS address propagation: a Pub-Sub `ADDRESS_CHANGE` channel broadcasts all address changes. The shipping system has a filter that passes only shipping addresses; the billing system has a filter that passes only billing addresses [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/content-based-router]] — more powerful alternative: routes to one of N channels rather than pass/drop
- [[wiki/concepts/message-channel]] — filter sits on a channel, upstream of a subscriber
- [[wiki/concepts/recipient-list]] — alternative approach: address messages to specific recipients directly

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — used in WGRUS address propagation to prevent billing addresses from reaching the shipping system and vice versa
