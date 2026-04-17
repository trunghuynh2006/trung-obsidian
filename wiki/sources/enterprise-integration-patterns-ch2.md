---
date: 2026-04-18
type: source
title: "Enterprise Integration Patterns — Chapter 2: Integration Styles"
source_file: raw/sources/enterprise.md
date_ingested: 2026-04-18
tags: [enterprise-integration, messaging, software-architecture, patterns]
---

# Enterprise Integration Patterns — Chapter 2: Integration Styles

**Source:** [[raw/sources/enterprise.md]]
**Authors:** Gregor Hohpe, Bobby Woolf (File Transfer and RPI sections by Martin Fowler)
**Published:** 2004 (Addison-Wesley)
**Ingested:** 2026-04-18
**Tags:** #enterprise-integration #messaging #software-architecture #patterns

## Summary

Chapter 2 gives formal pattern treatment to the four application integration styles introduced briefly in Chapter 1. Each style is presented with a problem statement, forces, solution, and consequences — enabling architects to reason about which style fits a given integration opportunity.

The chapter opens with seven decision criteria for evaluating integration approaches (coupling, simplicity, technology overhead, data format, timeliness, data-vs-functionality, asynchronicity), then applies those criteria to contrast the four styles.

The central argument: the four styles form a progression of sophistication. File Transfer is the simplest but stalest. Shared Database is timely but creates schema coupling. Remote Procedure Invocation adds encapsulation but keeps temporal coupling. Messaging combines timeliness, decoupling, and asynchronicity — at the cost of complexity and a learning curve. The book then focuses exclusively on Messaging, which it considers the best general-purpose integration approach.

## Key Points

- **Seven integration criteria:** coupling, simplicity, integration technology required, data format agreement, data timeliness, data vs. functionality sharing, asynchronicity.
- File Transfer: no specialized infrastructure; apps stay fully independent; but staleness is the core problem — and staleness causes data inconsistency that compounds over time.
- Shared Database: always consistent; SQL is universal; but unified schema design is politically contentious and technically hard; packages resist it; locking creates performance bottlenecks.
- Remote Procedure Invocation: applies OO encapsulation to integration; SOAP/CORBA/RMI; but the "looks like a local call" abstraction is deceptive — remote calls fail and timeout in ways local calls never do.
- Messaging: asynchronous, fine-grained, transformable, decoupled; reduces coupling to the minimum; but requires infrastructure, async mental model, and produces integration "glue code."
- The four styles are not mutually exclusive — a single integration solution may combine multiple styles at different integration points.
- Messaging can be thought of as "File Transfer where you produce a file with every change" — once files become fine-grained enough, they become messages and you need infrastructure to manage them.

## Patterns Introduced

- [[wiki/concepts/file-transfer]] — file-based integration; universal, decoupled, but infrequent and stale
- [[wiki/concepts/shared-database]] — single common DB; always consistent, but schema coupling and performance problems
- [[wiki/concepts/remote-procedure-invocation]] — encapsulated API calls across apps; timely but still tightly coupled
- [[wiki/concepts/messaging-integration]] — async message passing; best overall for loose coupling + timeliness

## Connections

- [[wiki/concepts/enterprise-application-integration]] — Chapter 2 adds the 7 integration criteria and upgrades the 4-style comparison with full pattern rigor
- [[wiki/concepts/loose-coupling]] — the key design goal that differentiates the four styles
- [[wiki/entities/gregor-hohpe]] — primary author
- [[wiki/entities/bobby-woolf]] — co-author
- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced the 4 styles briefly; Ch2 gives them full pattern treatment

## Quotes

> "The trick is not to choose the one style to use always, but to choose the best style for a particular integration opportunity."

> "Asynchronous messaging is fundamentally a pragmatic reaction to the problems of distributed systems."

> "Remote calls are slower, and can fail. With multiple applications communicating across an enterprise, you don't want one application's failure to bring down all of the other applications."

> "Once you get to fine grained files like this, it's easier to think of them as Messaging."
