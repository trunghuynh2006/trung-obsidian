---
date: 2026-04-22
type: concept
name: Event Sourcing
aliases: [Event Sourcing Pattern, Event Store, Append-Only Log]
tags: [software-architecture, design-patterns, data, distributed-systems, audit]
sources: 1
---

# Event Sourcing

## Definition
A data persistence pattern that stores the sequence of events that produced the current state, rather than only the current state itself. Current state is reconstructed by replaying the event log from the beginning (or from a snapshot). Enables complete audit trails, temporal queries, and multiple optimized read projections from a single source of truth.

## Detail

**Core mechanics:**
1. Every state change is captured as an **immutable event** object (`AccountOpenedEvent`, `MoneyDepositedEvent`, `MoneyWithdrawnEvent`).
2. Events are appended to an **event store** — an append-only log keyed by aggregate ID.
3. **Aggregates** apply events to update their in-memory state and produce events in response to commands.
4. To load an aggregate, replay all its stored events in order (or start from the latest snapshot).

**Benefits:**
- **Complete audit trail** — nothing is overwritten; the event log is the system of record.
- **Temporal queries** — reconstruct any aggregate's state at any point in time by filtering events by timestamp.
- **Multiple projections** — the same event stream feeds multiple optimized read models for different query patterns.
- **Debugging and replay** — events can be replayed to reproduce issues or rebuild corrupted read models.
- **Natural event-driven integration** — domain events are published to subscribers (read-model updaters, downstream services, analytics pipelines).

**Trade-offs:**
- Read performance requires pre-built projections; you cannot query current state directly from the event log.
- Long event histories need snapshots to avoid expensive full replays.
- Schema evolution (changing event formats over time) requires versioning and migration strategies.
- Conceptually more complex than CRUD for simple domains.

**Constituents:**
- `Event` base class — `eventId`, `aggregateId`, `timestamp`, `version`
- Domain events — `AccountOpenedEvent`, `MoneyDepositedEvent`, etc.
- Aggregate — applies events to build state; tracks uncommitted events produced by commands
- `EventStore` interface — `saveEvents(aggregateId, events, expectedVersion)`, `getEvents(aggregateId)`
- Repository — loads aggregate by replaying events from store
- Projections/handlers — subscribe to events and update read models

## Evidence & Examples

Temporal query — reconstruct account state at a specific past moment:
```java
public BankAccount findByIdAtTime(String accountId, Instant timestamp) {
    List<Event> filtered = eventStore.getEvents(accountId).stream()
        .filter(e -> !e.getTimestamp().isAfter(timestamp))
        .collect(toList());
    return BankAccount.fromEvents(filtered);
}
```

Aggregate command → event → state update:
```java
public void deposit(BigDecimal amount, String description) {
    applyEvent(new MoneyDepositedEvent(accountId, version + 1, amount, description));
}
private void applyEvent(Event event) {
    if (event instanceof MoneyDepositedEvent)
        this.balance = this.balance.add(((MoneyDepositedEvent) event).getAmount());
    this.version = event.getVersion();
    this.uncommittedEvents.add(event);
}
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/cqrs]] — the natural companion: write side stores events; read side builds projections. Combined form: [[wiki/concepts/cqrs-event-sourcing]]
- [[wiki/concepts/observer-pattern]] — read-model projections are observers of the event stream
- [[wiki/concepts/saga-pattern]] — saga log is a lightweight form of event sourcing for distributed transaction state
- [[wiki/concepts/messaging-integration]] — event stores integrate with message brokers for downstream event publication and subscription
- [[wiki/concepts/repository-pattern]] — an event-sourced repository loads aggregates by replaying events rather than reading current state

## Sources
- [[wiki/sources/design-patterns-reimagined]] — BankAccount aggregate, AccountOpenedEvent / MoneyDepositedEvent / MoneyWithdrawnEvent, EventStore interface, BankAccountRepository, temporal query, EventSourcingExample usage
