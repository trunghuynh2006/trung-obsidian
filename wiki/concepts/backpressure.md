---
date: 2026-04-22
type: concept
name: Backpressure
aliases: [Backpressure Pattern, Flow Control, Reactive Backpressure, Demand-Driven Streaming]
tags: [software-architecture, design-patterns, reactive, concurrency, streaming]
sources: 1
---

# Backpressure

## Definition
A flow control mechanism in reactive and streaming systems that allows a slow consumer to signal to a fast producer to reduce its output rate, preventing buffer overflow and system instability. A core primitive of the Reactive Streams specification.

## Detail

**The problem:** In a push-based pipeline, if a producer generates data faster than a consumer can process it, the consumer's buffer grows unbounded — eventually exhausting memory or causing silent data loss. This is a common failure mode in event pipelines, log processing, WebSocket streams, and high-throughput data ingestion.

**The solution — pull-based demand signaling:** The **Reactive Streams specification** (standardized as Java `java.util.concurrent.Flow`, and implemented by RxJava, Project Reactor, Akka Streams) gives consumers explicit control:
- `Subscriber.onSubscribe(Subscription)` — called once at subscription time
- `Subscription.request(n)` — consumer asks for exactly `n` more items; publisher sends at most `n`
- `Publisher.onNext(item)` — delivers one item, but only when demanded

**Buffering strategies** when consumer is temporarily behind:
- **Drop oldest** — evict the oldest buffered item when full; best for "latest value wins" use cases (sensor readings, UI state)
- **Drop newest** — reject incoming items when buffer full; best for time-sensitive data where old items are more valuable
- **Sampling** — skip items dynamically; increase skip rate when buffer is full, decrease when there is room

**Adaptive subscribers** monitor processing time per batch and dynamically adjust their request size: increase when processing is fast, decrease when processing is slow.

**Constituents:**
- Publisher — produces items; sends only when demanded
- Subscriber — processes items; controls demand via `Subscription.request(n)`
- Subscription — the link carrying demand signals from subscriber to publisher
- Buffer — intermediate storage with configurable size and overflow strategy

## Evidence & Examples

Adaptive subscriber adjusting request batch size based on measured processing throughput:
```java
private void adjustRequestSize() {
    long avgMsPerItem = timeTaken / currentRequestSize;
    if (avgMsPerItem < 10 && currentRequestSize < maxRequestSize)
        currentRequestSize = Math.min(currentRequestSize * 2, maxRequestSize);
    else if (avgMsPerItem > 100 && currentRequestSize > minRequestSize)
        currentRequestSize = Math.max(currentRequestSize / 2, minRequestSize);
}
```

DropOldest buffer (ring-buffer semantics for latest-value streams):
```java
public synchronized boolean offer(T item) {
    if (buffer.size() >= maxSize) buffer.poll(); // evict oldest
    return buffer.offer(item);
}
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/observer-pattern]] — backpressure is the key capability reactive streams add over classic synchronous Observer
- [[wiki/concepts/actor-model]] — actor mailboxes are bounded queues; backpressure in actor systems is enforced by rejecting messages when the mailbox is full
- [[wiki/concepts/async-await]] — async-await handles individual futures; backpressure handles continuous streams of items
- [[wiki/concepts/messaging-integration]] — message brokers implement backpressure via consumer offsets (Kafka), prefetch counts (RabbitMQ), and flow control acknowledgements

## Sources
- [[wiki/sources/design-patterns-reimagined]] — BackpressureAwarePublisher, BackpressureAwareSubscriber, AdaptiveBackpressureSubscriber, and three buffering strategy classes (DropOldest, DropNewest, Sampling)
