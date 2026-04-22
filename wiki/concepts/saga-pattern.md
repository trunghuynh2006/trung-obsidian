---
date: 2026-04-22
type: concept
name: Saga Pattern
aliases: [Saga, Distributed Saga, Compensating Transactions, Saga Orchestration, Saga Choreography]
tags: [software-architecture, design-patterns, distributed-systems, transactions, microservices]
sources: 1
---

# Saga Pattern

## Definition
A pattern for managing distributed transactions across multiple microservices. Each step executes as a local transaction; if any step fails, the saga executes compensating transactions in reverse order to undo completed steps. Ensures consistency without distributed locking or two-phase commit.

## Detail

**Why traditional ACID breaks down in microservices:** Two-phase commit (2PC) requires holding locks across services, reducing availability and creating tight coupling. In microservices, the Saga pattern replaces 2PC with a sequence of local transactions, each owned by a single service, coordinated through either orchestration or choreography.

**Two coordination approaches:**

**Orchestration** — A central saga orchestrator sends commands to services and tracks responses. Pros: explicit control flow, easy to observe and debug, single place to reason about the transaction. Cons: orchestrator is a coupling point.

**Choreography** — Services react to domain events emitted by prior steps; no central coordinator. Pros: fully decoupled services. Cons: control flow is implicit and harder to trace; eventual consistency is harder to reason about.

**Compensating transactions** are the critical invariant: every forward step must have a corresponding compensation operation:
- Reserve inventory → Release reservation
- Process payment → Refund payment
- Create shipment → Cancel shipment

Compensations must be idempotent and always succeed (or log failure and continue with others — never block the compensation chain).

**Saga log** — the orchestrator logs step start, completion, and compensation status. Essential for recovery from mid-saga process crashes.

**Constituents:**
- `SagaStep` — interface with `execute(context)` and `compensate(context)` methods
- `SagaContext` — shared map carrying data produced by each step (IDs, amounts, etc.)
- `SagaOrchestrator` — iterates steps; on failure, compensates all completed steps in reverse
- `SagaLog` — persists saga progress for crash recovery

## Evidence & Examples

Order-processing saga (Reserve Inventory → Process Payment → Create Shipment). Payment failure triggers automatic inventory release:
```java
public SagaResult execute(SagaContext ctx) {
    for (SagaStep step : steps) {
        try { step.execute(ctx); completedSteps.add(step); }
        catch (Exception e) { compensate(ctx, completedSteps); return SagaResult.failed(...); }
    }
    return SagaResult.success();
}
private void compensate(SagaContext ctx, List<SagaStep> done) {
    for (int i = done.size()-1; i >= 0; i--) done.get(i).compensate(ctx);
}
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/event-sourcing]] — choreography-style sagas emit domain events; event sourcing provides the durable event store enabling saga replay
- [[wiki/concepts/cqrs]] — saga coordinators issue commands; CQRS command handlers execute them
- [[wiki/concepts/circuit-breaker]] — circuit breakers wrap individual saga steps to prevent cascading failures mid-transaction
- [[wiki/concepts/messaging-integration]] — saga choreography runs over async messaging channels (Kafka topics, message queues)
- [[wiki/concepts/process-manager]] — EAI Process Manager and Saga orchestrator solve the same stateful coordination problem at different layers of the stack

## Sources
- [[wiki/sources/design-patterns-reimagined]] — orchestration-style saga with SagaStep, SagaContext, SagaOrchestrator, and three order-processing steps (ReserveInventory, ProcessPayment, CreateShipment)
