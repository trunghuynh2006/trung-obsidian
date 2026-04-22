---
date: 2026-04-22
type: concept
name: Singleton Pattern
aliases: [Singleton]
tags: [software-architecture, design-patterns, creational, anti-pattern, oop]
sources: 1
---

# Singleton Pattern

## Definition
A creational pattern (Gang of Four, 1994) that ensures a class has only one instance and provides a global point of access to it. Now widely regarded as an **anti-pattern** in modern software development.

## Detail
The Singleton conflates two separate responsibilities: (1) enforcing that only one instance exists, and (2) providing global access to that instance. The global access creates tight coupling throughout the codebase — any code that calls `getInstance()` carries a hidden, non-injectable dependency not visible in constructor signatures. The classic lazy-initialization form is also not thread-safe.

The legitimate need Singleton addressed — ensuring a shared resource (database connection, config, logger) has a single coordinated lifecycle — is now handled by **dependency injection containers**, which manage scope as a configuration concern rather than baking it into the class structure. A DI container can create a singleton-scoped bean while keeping the class itself ignorant of its own lifecycle.

**Common failure modes:**
- Hidden dependencies invisible in constructor signatures
- Cannot substitute a mock for testing
- Global mutable state breaks reasoning in concurrent systems
- Lazy initialization adds synchronization complexity

## Evidence & Examples

Classic implementation (problematic):
```java
public class DatabaseConnection {
    private static DatabaseConnection instance;
    public static DatabaseConnection getInstance() {
        if (instance == null) instance = new DatabaseConnection();
        return instance;
    }
}
```

Modern replacement — explicit DI (dependency visible in constructor; DI container manages lifecycle):
```java
public class OrderService {
    public OrderService(DatabaseConnection database) { this.database = database; }
}
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/loose-coupling]] — Singleton violates loose coupling by creating hidden global access
- [[wiki/concepts/abstract-factory-pattern]] — another GoF creational pattern removed from the modern catalog
- [[wiki/concepts/repository-pattern]] — Repository instances are often DI-managed singletons — correctly, as a container concern rather than a class-level Singleton

## Contradictions
None. Removal from the modern catalog is consensus in mainstream software engineering.

## Sources
- [[wiki/sources/design-patterns-reimagined]] — identifies Singleton as the first pattern to be removed from a modern catalog; DI replacement example in Java
