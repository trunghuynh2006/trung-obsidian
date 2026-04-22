---
date: 2026-04-22
type: concept
name: Repository Pattern
aliases: [Repository, Unit of Work, Specification Pattern, Data Repository]
tags: [software-architecture, design-patterns, data, domain-driven-design, behavioral]
sources: 1
---

# Repository Pattern

## Definition
A data-access pattern that provides a collection-like interface for accessing domain objects, encapsulating the details of data storage and retrieval. Modern implementations add Specification-based composable queries, transparent caching, and Unit of Work coordination.

## Detail

The Repository pattern has roots in Martin Fowler's *Patterns of Enterprise Application Architecture* (2003). The modern form is significantly richer.

**Core intent:** Separate domain model from data-access concerns. Business logic references a `CustomerRepository` interface; the implementation handles SQL, NoSQL, caching, or any combination. This enables swapping persistence mechanisms without touching business logic, and injecting mocks for testing.

**Modern additions:**

**Specification pattern** — composable query predicates that avoid polluting the repository interface with dozens of `findByX` methods. Specifications implement a `isSatisfiedBy(entity)` predicate and compose with `.and()`, `.or()`, `.not()`:
```java
Specification<Customer> spec = new CustomerByStatusSpec(ACTIVE)
    .and(new CustomerByEmailDomainSpec("example.com"));
repository.findBySpecification(spec);
```

**Caching layer** — repositories can transparently cache frequently accessed entities with TTL-based invalidation. When a cache entry expires or is missing, the repository loads from the underlying store and repopulates the cache. A max-size eviction policy removes the least recently written entry when the cache is full.

**Unit of Work** — tracks which entities have been created, modified, or deleted during a business operation and flushes all changes in a single `commit()` call. If the operation fails, `rollback()` clears all tracked changes. This provides transaction-like semantics without requiring a database transaction to span the entire business operation.

**Constituents:**
- Repository interface — `save`, `delete`, `findById`, `findAll`, `findBySpecification`
- Concrete implementation — handles actual storage with optional caching
- Specification — composable predicate over domain objects
- Cache layer — TTL + size-bounded transparent cache
- Unit of Work — change tracker (`registerNew`, `registerModified`, `registerDeleted`, `commit`, `rollback`)

## Evidence & Examples

Composable specification query:
```java
Specification<Customer> complexSpec =
    new CustomerByStatusSpec(ACTIVE)
    .or(new CustomerByStatusSpec(SUSPENDED))
    .and(new CustomerByEmailDomainSpec("example.com"));
List<Customer> result = repository.findBySpecification(complexSpec);
```

Unit of Work coordinating multiple changes:
```java
unitOfWork.registerNew(customer1);
unitOfWork.registerNew(customer2);
customer3.setStatus(CustomerStatus.SUSPENDED);
unitOfWork.registerModified(customer3);
unitOfWork.commit();  // saves all three in one batch
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/event-sourcing]] — an event-sourced repository loads aggregates by replaying their event history rather than reading current state
- [[wiki/concepts/cqrs]] — CQRS splits repository responsibilities: write-side repository enforces consistency; read-side repository optimizes for query patterns
- [[wiki/concepts/loose-coupling]] — Repository hides the persistence layer behind an interface; the canonical loose-coupling technique for data access
- [[wiki/concepts/singleton-pattern]] — Repository instances are often DI-managed singletons — correctly, as a container concern rather than a Singleton class

## Sources
- [[wiki/sources/design-patterns-reimagined]] — CachedCustomerRepository, Specification with and/or/not composition, UnitOfWork; Customer domain model with CustomerStatus enum
