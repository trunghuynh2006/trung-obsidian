---
date: 2026-04-22
type: concept
name: CQRS
aliases: [Command Query Responsibility Segregation, Command Pattern, CQRS Pattern]
tags: [software-architecture, design-patterns, distributed-systems, behavioral, data]
sources: 1
---

# CQRS — Command Query Responsibility Segregation

## Definition
An architectural pattern derived from the Gang of Four Command pattern. CQRS separates operations that **change state** (commands) from operations that **read state** (queries), allowing each side to be modeled, scaled, and optimized independently.

## Detail

**Classic Command pattern:** Encapsulates a request as an object with an `execute()` and optional `undo()` method, supporting parameterization, queuing, logging, and undo. The classic form made no distinction between reading and writing — both flowed through the same unified object model and data store.

**Modern transformation to CQRS:** The read and write requirements of most applications differ fundamentally:
- **Write side** needs business rule validation, consistency enforcement, and transactional safety.
- **Read side** needs speed, denormalized views, and query-specific schemas.

CQRS formalizes this split:
- **Commands** — plain objects expressing intent to change state (no return value beyond an acknowledgement). Processed by command handlers that load aggregates, validate rules, persist changes, and publish domain events.
- **Queries** — plain objects requesting data. Processed by query handlers that read from optimized read models, which may use a different database, schema, or index than the write model.

**Key consequence:** eventual consistency between write and read sides. Read models are updated asynchronously after write-side events are published. This is the main trade-off versus simpler CRUD architectures.

**When to use CQRS:**
- High read-to-write ratios where read optimization is critical
- Multiple different query patterns over the same data
- Systems already using event-driven architecture
- Domain with complex business rules on writes and simple reporting on reads

**Combination with Event Sourcing:** The write side naturally stores events; read-side projections consume them. See [[wiki/concepts/cqrs-event-sourcing]].

## Evidence & Examples

```java
// Command: represents intent to change state
public class TransferMoneyCommand {
    private final String sourceAccountId, destinationAccountId;
    private final BigDecimal amount;
    private final String transactionId = UUID.randomUUID().toString();
}

// Command handler: validates rules, updates write model, publishes events
public class TransferMoneyCommandHandler {
    public CommandResult handle(TransferMoneyCommand cmd) {
        Account source = accountRepository.findById(cmd.getSourceAccountId());
        if (source.getBalance().compareTo(cmd.getAmount()) < 0) return CommandResult.failure("Insufficient funds");
        source.withdraw(cmd.getAmount());
        accountRepository.save(source);
        eventPublisher.publish(new MoneyTransferredEvent(...));
        return CommandResult.success(cmd.getTransactionId());
    }
}

// Query handler: reads from denormalized read model (not the write store)
public class GetAccountBalanceQueryHandler {
    public AccountBalanceDTO handle(GetAccountBalanceQuery q) {
        return readRepository.findById(q.getAccountId());
    }
}
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/event-sourcing]] — write-side events naturally feed an event-sourcing store; CQRS+ES is the common production combination
- [[wiki/concepts/observer-pattern]] — read-model projections are observers of the write side's event stream
- [[wiki/concepts/saga-pattern]] — saga coordinators issue commands and react to their outcomes
- [[wiki/concepts/loose-coupling]] — CQRS decouples read and write scaling, schema, and infrastructure concerns
- [[wiki/concepts/messaging-integration]] — CQRS event publication maps to the async messaging integration style

## Sources
- [[wiki/sources/design-patterns-reimagined]] — traces Command → CQRS transformation with full Java code comparison; TransferMoneyCommand, TransferMoneyCommandHandler, GetAccountBalanceQueryHandler
