---
date: 2026-04-18
type: concept
name: Content Enricher
aliases: [message enricher, data enricher]
tags: [enterprise-integration, messaging, patterns, transformation]
sources: 1
---

# Content Enricher

## Definition

A component that adds missing data items to an incoming message before forwarding it, so downstream components have all the information they need.

## Detail

A Content Enricher adds data that was not in the original message — either by generating it (e.g., assigning a unique ID) or by looking it up from an external source (e.g., fetching a customer's credit score, looking up a postal code).

**Why needed?** The original sender may not have all the data that downstream steps require. Rather than requiring the sender to know about downstream needs (coupling), the enricher fills in the gaps at the right point in the pipeline.

**Common use case: correlation IDs.** Before splitting a message into parts (see [[wiki/concepts/splitter]]), you need a unique identifier to correlate the parts back together in the [[wiki/concepts/aggregator]]. The Content Enricher generates and stamps this ID.

**Relationship to Claim Check:** The Content Enricher adds data inline to the message. The [[wiki/concepts/claim-check]] is the inverse: strips data out of the message, stores it centrally, and passes a reference. Together they form the full "store/retrieve" pattern.

## Evidence & Examples

- WGRUS: a Content Enricher is inserted into the order-taking pipeline to generate a unique `OrderID` for each incoming order. Without it, the downstream Aggregator cannot correlate split `OrderItem` results back to the correct order [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/splitter]] — typically used immediately after the Content Enricher (enrich → split → route → aggregate)
- [[wiki/concepts/aggregator]] — uses the correlation ID added by the Content Enricher
- [[wiki/concepts/claim-check]] — the inverse: strips data from the message and stores it centrally
- [[wiki/concepts/message-translator]] — also transforms messages, but via format conversion, not data addition

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS multi-item order pipeline to add unique order ID before splitting
