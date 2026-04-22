---
date: 2026-04-22
type: concept
name: Observer Pattern
aliases: [Observer, Reactive Streams, Publish-Subscribe, Event-Driven Architecture]
tags: [software-architecture, design-patterns, behavioral, reactive, distributed]
sources: 1
---

# Observer Pattern

## Definition
A behavioral pattern (Gang of Four, 1994) that defines a one-to-many dependency so that when one object changes state, all dependents are notified automatically. In modern systems, evolved into reactive streams, event buses, and distributed publish-subscribe architectures.

## Detail

**Classic form:** A `Subject` holds a `List<Observer>` and calls `update()` on each when its state changes. Notification is synchronous and blocking — the subject waits until all observers finish. No built-in error handling, no backpressure, no thread-safety guarantees, and memory leaks occur when observers are not explicitly detached.

**Modern transformation across three layers:**

**1. Reactive Streams** (RxJava, Project Reactor, Java `Flow` API) — asynchronous, non-blocking event delivery with backpressure support, error semantics (`onError`), completion signals (`onComplete`), and composable transformation operators (`filter`, `map`, `debounce`, `merge`, `throttle`). Subscribers control their own consumption rate via demand signals.

**2. In-process event buses** (Guava EventBus, Spring ApplicationEvents) — fire-and-forget dispatching within a single JVM; decouples event producers from handlers without the full reactive machinery.

**3. Distributed publish-subscribe** (Apache Kafka, RabbitMQ, AWS SNS/SQS, Azure Service Bus) — events published to message brokers; subscribers can be in different processes, machines, or data centers; brokers handle delivery guarantees, persistence, replay, and independent scaling of producers and consumers. This is the foundation of modern microservices event-driven architecture.

Reactive streams add capabilities the classic pattern lacked:
- Asynchronous, non-blocking delivery
- **Backpressure** — consumers control inflow rate (see [[wiki/concepts/backpressure]])
- Error and completion semantics built into the stream contract
- Operator pipeline for transformation, filtering, combining, and rate-limiting

## Evidence & Examples

Classic (synchronous, blocking — all observers run on the subject's thread):
```java
private void notifyObservers() {
    for (Observer observer : observers) { observer.update(state); }
}
```

Modern reactive (operators applied per subscriber; async delivery):
```java
subject.getObservable()
    .filter(msg -> msg.length() > 5)
    .map(String::toUpperCase)
    .debounce(100, TimeUnit.MILLISECONDS)
    .subscribe(message -> ..., error -> ..., () -> ...);
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/backpressure]] — backpressure is the key capability reactive streams add over classic Observer
- [[wiki/concepts/messaging-integration]] — distributed pub-sub (Kafka, RabbitMQ) is Observer at the integration layer
- [[wiki/concepts/event-sourcing]] — event sourcing publishes domain events that observers / projections consume
- [[wiki/concepts/actor-model]] — Actor mailboxes implement a related async-message-passing model without shared state
- [[wiki/concepts/cqrs]] — CQRS read-model projections are Observer-pattern subscribers on the write side's event stream

## Sources
- [[wiki/sources/design-patterns-reimagined]] — traces Observer evolution from synchronous notification list to reactive streams with operators, and to distributed pub-sub over message brokers
