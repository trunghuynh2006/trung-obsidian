---
date: 2026-04-22
type: concept
name: Strategy Pattern
aliases: [Strategy, Functional Strategy, Higher-Order Functions as Strategy]
tags: [software-architecture, design-patterns, behavioral, functional-programming]
sources: 1
---

# Strategy Pattern

## Definition
A behavioral pattern (Gang of Four, 1994) that defines a family of algorithms, encapsulates each one, and makes them interchangeable at runtime. In modern languages with first-class functions, the class-hierarchy implementation is largely replaced by higher-order functions and lambdas.

## Detail

**Classic form:** Define a `Strategy` interface and one concrete class per algorithm variant. A context object holds a strategy reference that can be set or injected at runtime. The intent is sound — vary the algorithm independently of the client — but the implementation forces a separate class for every variant, even trivial ones.

**Modern transformation:** Languages with first-class functions (Java 8+, Kotlin, Python, TypeScript, Go, C#) make strategy a function parameter. There is no need for a `PaymentStrategy` interface plus `CreditCardStrategy` and `PayPalStrategy` classes:

```java
// Use a method reference
cart.setPaymentStrategy(PaymentStrategies::payCreditCard);

// Use a lambda
cart.setPaymentStrategy((details, amount) -> processBankTransfer(details, amount));

// Compose strategies
cart.setPaymentStrategy(loggingStrategy.andThen(actualPayment));
```

The result is less code, clearer intent, easier testing (pass any function), and better composability.

**When the class form is still appropriate:** When a strategy carries substantial state constructed at creation time (e.g., a pre-loaded ML model, a compiled regex, a configured HTTP client), encapsulating it in a class is natural. For stateless algorithms, prefer functions.

## Evidence & Examples

Classic (one class per variant — verbose):
```java
public class CreditCardStrategy implements PaymentStrategy {
    private String cardNumber, cvv;
    public void pay(double amount) { ... }
}
```

Modern (function parameter — concise and composable):
```java
public class ModernShoppingCart {
    private BiConsumer<PaymentDetails, Double> paymentStrategy;
    public void checkout(PaymentDetails details, double amount) {
        paymentStrategy.accept(details, amount);
    }
}
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/observer-pattern]] — reactive stream operators are Strategy-like higher-order functions applied to event streams
- [[wiki/concepts/cqrs]] — command and query handlers implement a similar strategy dispatch: incoming object type selects the handler function
- [[wiki/concepts/abstract-factory-pattern]] — both patterns involve selecting among variants at runtime; Strategy does it for behavior, Abstract Factory for object creation

## Sources
- [[wiki/sources/design-patterns-reimagined]] — side-by-side Java comparison of class-based vs. lambda-based Strategy; method references, lambdas, and `BiConsumer.andThen()` composition
