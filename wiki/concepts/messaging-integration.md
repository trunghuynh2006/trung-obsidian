---
date: 2026-04-18
type: concept
name: Messaging (Integration Style)
aliases: [Messaging, asynchronous messaging, message-oriented middleware, MOM]
tags: [enterprise-integration, integration-styles, patterns]
sources: 1
---

# Messaging (Integration Style)

## Definition

An integration style where applications communicate by exchanging discrete packets of data (messages) through a messaging system asynchronously — without requiring both sides to be available simultaneously.

## Detail

**How it works:** Applications connect to a shared messaging infrastructure. A sender deposits a message on a channel; the messaging system holds it until the receiver is ready to consume it. The transfer is asynchronous — the sender does not wait for the receiver to process the message.

**Why it's the recommended style (Hohpe & Woolf's argument):**
- **vs. File Transfer**: Same decoupling, but frequent/immediate instead of batch/stale. "Messaging is File Transfer where you produce a file with every change."
- **vs. Shared Database**: Same timeliness, but no shared schema — each app keeps its own data model; a Message Translator bridges formats at the boundary.
- **vs. Remote Procedure Invocation**: Same ability to invoke behavior, but async — the sender does not block, and the receiver's temporary unavailability doesn't break the sender.

**Seven-criteria assessment:**

| Criterion | Rating | Notes |
|-----------|--------|-------|
| Coupling | ✅ Very low | No shared schema; no direct API dependency; no temporal dependency |
| Simplicity | ❌ Low | Async mental model is unfamiliar; requires infrastructure; produces glue code |
| Integration technology | ❌ Requires MOM | Message broker / messaging middleware is a real infrastructure cost |
| Data format | ✅ Flexible | Message Translators bridge formats; Canonical Data Model unifies |
| Timeliness | ✅ High | Messages sent immediately on change; received as soon as consumer is ready |
| Data-vs-functionality | ✅ Both | Document Messages share data; Command Messages invoke behavior |
| Asynchronicity | ✅ Fully async | Sender and receiver are temporally decoupled |

**Four coupling dimensions eliminated:**
- **Platform**: messages use agreed serialization (XML, JSON), not internal memory format
- **Location**: apps address logical channels, not physical machine addresses
- **Time**: sender deposits message; receiver consumes it whenever ready (even hours later)
- **Data format**: Message Translators convert at boundaries; Canonical Data Model unifies

**Costs:**
- **Async learning curve**: most developers are trained on synchronous, procedural code; async design requires different patterns for error handling, correlation, and ordering.
- **Debugging complexity**: messages may traverse multiple hops; failures are harder to trace.
- **Glue code**: integrators still write transformation, routing, and endpoint code. Messaging provides the infrastructure; it doesn't write the logic.
- **Lag**: even with frequent messaging, there is always *some* propagation delay — applications are never perfectly in sync.

**This concept vs. the pattern catalog:** This page describes Messaging as an *integration style* (the fourth of four, and the recommended one). The detailed *how-to* of messaging — channels, routers, translators, aggregators, etc. — is covered in the pattern catalog started in Chapter 1 and Chapter 3+. See [[wiki/concepts/message]], [[wiki/concepts/message-channel]], etc.

## When to use

- Most enterprise application integration scenarios — the book's default recommendation
- When temporal decoupling is important (receiver may be down or slow)
- When multiple apps need to react to the same event (Pub-Sub)
- When you need to decouple the data format of sender from receiver

## Connections

- [[wiki/concepts/file-transfer]] — predecessor; same decoupling, worse timeliness
- [[wiki/concepts/shared-database]] — predecessor; same timeliness, schema coupling
- [[wiki/concepts/remote-procedure-invocation]] — predecessor; same functionality-sharing, temporal coupling
- [[wiki/concepts/loose-coupling]] — Messaging eliminates all four coupling dimensions
- [[wiki/concepts/message]] — the fundamental data unit
- [[wiki/concepts/message-channel]] — the conduit
- [[wiki/concepts/message-translator]] — bridges data format differences
- [[wiki/concepts/canonical-data-model]] — the shared-format alternative to Shared Database schema coupling
- [[wiki/concepts/enterprise-application-integration]] — one of four integration styles

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch2]] — full integration-style pattern treatment; comparison against other three styles
- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced as the solution to tight coupling; WGRUS example uses Messaging throughout
