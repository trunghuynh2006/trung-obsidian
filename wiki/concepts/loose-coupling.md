---
date: 2026-04-18
type: concept
name: Loose Coupling
aliases: [loose coupling, decoupling]
tags: [enterprise-integration, software-architecture]
sources: 1
---

# Loose Coupling

## Definition

A design principle that minimizes the assumptions two communicating parties (components, services, applications) make about each other, so each can evolve independently without breaking the other.

## Detail

Coupling is measured by the number of assumptions parties make. Every assumption is a dependency; every dependency is a potential breakage point.

**Four coupling dimensions** (Hohpe & Woolf):

| Dimension | Tightly coupled | Loosely coupled |
|-----------|----------------|-----------------|
| **Platform** | Sender uses same integer representation as receiver | Common serialization format (e.g., XML, JSON) |
| **Location** | Hard-coded IP/hostname | Logical channel address; DNS or directory indirection |
| **Time** | Sender and receiver must both be up simultaneously | Queued channel; receiver can be down, message waits |
| **Data format** | Exact parameter list must match | Translator layer; schema evolution without full breaks |

**Why RPC fails as a loose-coupling strategy:** Remote Procedure Call (CORBA, DCOM, .NET Remoting, RPC-style Web Services) attempts to make remote calls look like local calls. But remote calls violate every assumption local calls make: different language, order-of-magnitude slower, can fail mid-flight, network can partition. Hiding that mismatch creates brittle solutions that break in non-obvious ways.

**How messaging achieves loose coupling:**
1. Self-describing message format (XML, JSON) eliminates platform coupling.
2. Logical channel address eliminates location coupling.
3. Queued delivery eliminates temporal coupling.
4. Translator components at channel boundaries eliminate data-format coupling.

**Tradeoff:** Loose coupling adds complexity. A 10-line TCP/IP socket solution becomes a message broker + channel adapter + translator + router solution. This complexity is managed through middleware infrastructure and a shared pattern vocabulary.

## Evidence & Examples

- TCP/IP socket example in WGRUS: 10 lines of code, but fails on endianness, hard-coded hostname, synchronous dependency, fixed parameter order — four coupling dimensions violated simultaneously [[wiki/sources/enterprise-integration-patterns-ch1]]
- Waldo et al. (1994): "objects that interact in a distributed system need to be dealt with in ways that are intrinsically different" — the theoretical grounding cited by Hohpe [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/enterprise-application-integration]] — the domain where loose coupling is the primary design goal
- [[wiki/concepts/message-channel]] — the mechanism that achieves location and temporal decoupling
- [[wiki/concepts/message-translator]] — eliminates data-format coupling
- [[wiki/concepts/canonical-data-model]] — shared format that reduces translator complexity when many apps connect

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduces loose coupling as the core EAI principle; four-dimension taxonomy; 1 Minute EAI demonstration
