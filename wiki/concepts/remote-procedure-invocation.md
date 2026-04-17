---
date: 2026-04-18
type: concept
name: Remote Procedure Invocation
aliases: [RPI, RPC, Remote Procedure Call, Remote Method Invocation, RMI, Web Services RPC]
tags: [enterprise-integration, integration-styles, patterns]
sources: 1
---

# Remote Procedure Invocation (RPI)

## Definition

An integration style where each application exposes an interface (methods/procedures) that other applications can call remotely, applying the encapsulation principle of OO design across application boundaries.

## Detail

**How it works:** Each application is treated as a large-scale component with encapsulated data. It exposes an API. Other applications invoke that API to request data or trigger behavior. Technologies: CORBA, DCOM, Java RMI, .NET Remoting, SOAP/Web Services.

**Why it improves on Shared Database:** Encapsulation means each app controls its own data. Other apps cannot directly read or write the internal schema — they must go through the published API. This means the app can change its internal representation without breaking others, as long as the API contract stays stable.

**Seven-criteria assessment:**

| Criterion | Rating | Notes |
|-----------|--------|-------|
| Coupling | ⚠️ Medium | Less than Shared Database (no schema exposure), but API changes still ripple |
| Simplicity | ⚠️ Medium | Familiar to developers; but remote≠local is a trap |
| Integration technology | ⚠️ Requires framework | CORBA/SOAP/RMI stacks are non-trivial |
| Data format | ✅ Encapsulated | Each app converts internally; no shared schema |
| Timeliness | ✅ Immediate | Synchronous call; result arrives instantly |
| Data-vs-functionality | ✅ Both | Can invoke behavior, not just share data |
| Asynchronicity | ❌ Synchronous | Caller blocks until callee completes |

**The remote≠local trap (the core failure mode):** The appeal of RPI is that "it looks like a local call." This is also its biggest danger. Local calls are:
- Fast (nanoseconds); remote calls are slow (milliseconds to seconds)
- Reliable (same process, same memory); remote calls can timeout, fail mid-flight, or reach a dead server
- Sequential (same thread); remote calls introduce distributed system failure modes

Developers who design systems assuming remote calls behave like local calls produce brittle, slow, hard-to-debug integrations. Waldo et al. (1994): "objects that interact in a distributed system need to be dealt with in ways that are intrinsically different."

**Sequencing coupling:** Even without a shared schema, RPI creates sequencing dependencies. If App A must call App B before calling App C, changing the order requires changing App A. These sequencing assumptions accumulate and create "integration knots."

**SOAP/Web Services:** The most recent (at time of writing) incarnation of RPI. Valuable for firewall-friendliness (HTTP) and cross-platform reach. But adding WS-* extensions fragmented the standard, and RPC-style Web Services repeat the same remote≠local mistakes as CORBA.

## When to use

- You need to invoke behavior in another application, not just share data
- Low-latency, synchronous response is required (e.g., real-time price check at checkout)
- The other application's API is stable and under controlled governance
- The call volume is low enough that synchronous blocking is acceptable

## Connections

- [[wiki/concepts/file-transfer]] — simpler alternative; data-only
- [[wiki/concepts/shared-database]] — data-only; no encapsulation
- [[wiki/concepts/messaging-integration]] — the async alternative that avoids temporal coupling
- [[wiki/concepts/loose-coupling]] — RPI achieves some decoupling (encapsulation) but fails on temporal and location coupling
- [[wiki/concepts/enterprise-application-integration]] — one of four integration styles

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch2]] — full pattern treatment; written by Martin Fowler; remote≠local analysis; sequencing coupling
- [[wiki/sources/enterprise-integration-patterns-ch1]] — Ch1 introduced RPI failure modes (the "1 Minute EAI" TCP/IP example demonstrates tight coupling)
