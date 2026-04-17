---
date: 2026-04-18
type: concept
name: Return Address
aliases: [reply-to, reply channel, replyTo]
tags: [enterprise-integration, messaging, patterns, orchestration]
sources: 1
---

# Return Address

## Definition

A field in a request message that specifies the channel where the service should send its reply, allowing the same service to be reused by different callers each expecting replies on different channels.

## Detail

**The problem without Return Address:** A service hard-codes its reply channel. This means it can only be used by one type of caller — every other caller has to read from that fixed channel. Services become tightly coupled to their callers.

**With Return Address:** The service is completely decoupled from the reply destination. Each caller specifies a different `replyTo` channel. The service sends results wherever the caller says. This is what makes services genuinely reusable in a Service-Oriented Architecture.

**In a Process Manager context:** The Process Manager generates a unique reply channel per process instance, stamps it as the Return Address on each request, then listens to that channel for the reply. This is how it correlates responses back to the correct in-progress order.

**Legacy systems:** Most legacy systems were not built with Return Address in mind. Wrapping them with a [[wiki/concepts/smart-proxy]] adds this capability without changing the system.

**Relationship to Correlation ID:** Return Address tells a service *where* to send the reply. A Correlation ID (often included in the same message) tells the recipient *which request* the reply belongs to. Both are often needed together.

## Evidence & Examples

- WGRUS SOA design: each shared service (inventory, billing, shipping) must support Return Address so the Process Manager can route replies to the correct process instance [[wiki/sources/enterprise-integration-patterns-ch1]]
- WGRUS testing: the Test Data Generator specifies a special reply channel as the Return Address so test replies are separated from production replies [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/process-manager]] — primary consumer: uses Return Address to correlate service replies to process instances
- [[wiki/concepts/smart-proxy]] — adds Return Address support to legacy services that lack it
- [[wiki/concepts/message-channel]] — the reply channel referenced by the Return Address

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS SOA design and testing/monitoring section
