---
date: 2026-04-18
type: concept
name: Claim Check
aliases: [store/retrieve, message claim check]
tags: [enterprise-integration, messaging, patterns, transformation]
sources: 1
---

# Claim Check

## Definition

A pattern where a message's large or reusable data is stored in a central store and replaced with a reference (the "claim check") in the message body. Downstream components retrieve the full data when they need it.

## Detail

**The problem it solves:** In a multi-step message pipeline, every intermediate component must carry all the data from the original message forward — even data it doesn't use — so that the final consumer has everything it needs. This causes messages to bloat with irrelevant data and creates unnecessary coupling between steps.

**The solution:** Strip the bulky/shared data from the message and store it in a [[wiki/concepts/message-store]]. Include only a reference (a "claim check," like a coat-check token) in the message. Downstream components that need the full data retrieve it from the store using the reference.

**Benefits:**
- Reduces message size in the channel.
- Intermediate steps don't carry data they don't need.
- The store becomes a shared, authoritative record of the original data.

**Relationship to Content Enricher:** The Content Enricher adds data to a message. The Claim Check strips data from a message and stores it. Together they form a complete store/retrieve cycle: enrich at ingestion time, check in to the store, retrieve later.

**Relationship to Process Manager:** When the Claim Check store also tracks process state (which steps have completed), it becomes a [[wiki/concepts/process-manager]].

## Evidence & Examples

- WGRUS order tracking: instead of all intermediate messages carrying the full order data, the `NEW_ORDER` message is stored in a Message Store. Downstream steps reference the order ID to retrieve data; they no longer need to pass all fields through every hop [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/message-store]] — the store where claimed data is held
- [[wiki/concepts/content-enricher]] — the inverse: adds data inline to the message
- [[wiki/concepts/process-manager]] — a Message Store that also tracks process progress becomes a Process Manager

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS order status / message store section as a consequence of centralizing order data
