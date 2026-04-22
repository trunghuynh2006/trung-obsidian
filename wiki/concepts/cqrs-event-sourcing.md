---
date: 2026-04-22
type: concept
name: CQRS + Event Sourcing
aliases: [CQRS/ES, Event-Sourced CQRS, CQRS with Event Sourcing]
tags: [software-architecture, design-patterns, data, distributed-systems, audit]
sources: 1
---

# CQRS + Event Sourcing

## Definition
A combined architectural pattern where the write side of CQRS uses Event Sourcing to persist state as an immutable event log, while the read side builds multiple optimized projections from that event stream. Provides independent read/write scaling, complete audit trails, and multiple tailored read models from a single source of truth.

## Detail

**Why combine them:** CQRS separates read and write concerns. Event Sourcing provides a natural write-side persistence mechanism. Together they address the consistency-auditability-query-performance trilemma that neither pattern fully resolves alone:

| Concern | CQRS alone | Event Sourcing alone | Combined |
|---|---|---|---|
| Audit trail | Depends on write model | Yes — event log | Yes |
| Temporal queries | No | Yes | Yes |
| Multiple query patterns | Yes — separate read models | Requires projections | Yes — multiple projections |
| Write-side simplicity | Can use any storage | Complex — replaying events | Event log IS the write model |

**Flow:**
1. Client sends **command** → command handler loads aggregate from event store (by replaying events) → validates business rules → aggregate emits new events → events persisted to event store.
2. Events published to event bus → **event handlers** update one or more read-model projections asynchronously.
3. Client sends **query** → query service reads from the appropriate projection (not the event store directly).

**Multiple projections from one stream:** The same `MoneyDepositedEvent` can simultaneously update:
- `AccountBalanceReadModel` — current balance per account (for balance queries)
- `TransactionHistoryReadModel` — ordered list of transactions (for statement queries)
- A risk/fraud analysis model, a reporting aggregate, an analytics index, etc.

Each projection can be rebuilt from scratch by replaying the full event log if it becomes stale or corrupted.

**Trade-offs:**
- **Eventual consistency** — projections lag behind the write side by event processing time.
- **Complexity** — two separate codepaths (command/event vs. query), event schema versioning, projection rebuild strategies.
- **Best fit:** high read-to-write ratios, audit requirements, multiple distinct query patterns, systems where temporal queries are valuable (financial, medical, compliance domains).

## Evidence & Examples

Complete write + read roundtrip:
```java
// Write side: deposit command → event sourced
public void deposit(String accountId, BigDecimal amount, String desc) {
    BankAccount account = writeRepository.findById(accountId);  // loads by event replay
    account.deposit(amount, desc);                              // emits MoneyDepositedEvent
    writeRepository.save(account);                             // persists event
    account.getUncommittedEvents().forEach(readModelUpdater::handleEvent); // updates projections
}

// Read side: query hits projection, not event store
public Optional<BigDecimal> getBalance(String accountId) {
    return queryService.getAccountBalance(accountId);  // reads AccountBalanceReadModel
}
```

Two projections from the same event:
```java
// AccountBalanceReadModel: updateable balance counter
balanceModel.applyDeposit(event.getAmount(), event.getTimestamp());

// TransactionHistoryReadModel: append-only history
historyModel.addTransaction("DEPOSIT", event.getAmount(), event.getDescription(), event.getTimestamp());
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/cqrs]] — CQRS provides the read/write separation architecture
- [[wiki/concepts/event-sourcing]] — Event Sourcing provides the write-side persistence mechanism
- [[wiki/concepts/observer-pattern]] — read-model projections are observers of the event stream
- [[wiki/concepts/repository-pattern]] — write-side repository is event-sourced; read-side repository reads from projections
- [[wiki/concepts/saga-pattern]] — in CQRS+ES systems, sagas coordinate multi-step workflows by issuing commands and subscribing to domain events

## Sources
- [[wiki/sources/design-patterns-reimagined]] — CQRSBankingSystem full implementation; AccountBalanceReadModel, TransactionHistoryReadModel, AccountReadModelUpdater, AccountQueryService; two projections from one event stream
