---
date: 2026-04-22
type: concept
name: Circuit Breaker Pattern
aliases: [Circuit Breaker, Hystrix, Resilience4j]
tags: [software-architecture, design-patterns, distributed-systems, resilience, fault-tolerance]
sources: 1
---

# Circuit Breaker Pattern

## Definition
A resilience pattern for distributed systems that prevents an application from repeatedly attempting an operation likely to fail, allowing it to fail fast and recover gracefully. Not in the original GoF catalog; fundamental to modern microservices architecture.

## Detail

Named after an electrical circuit breaker. The pattern is a **three-state finite automaton**:

1. **CLOSED** (normal operation) — requests pass through; failures are counted. When the failure count exceeds `failureThreshold`, the circuit trips to OPEN.
2. **OPEN** (failing fast) — all requests are immediately rejected with an error, without attempting the operation. Prevents cascading failures and gives the failing service time to recover.
3. **HALF-OPEN** (recovery probe) — after a `timeout` period, a limited number of test requests are allowed through. If `successThreshold` consecutive requests succeed, the circuit resets to CLOSED. If any fail, the circuit returns to OPEN.

**Why it matters:** In synchronous microservice calls, a slow or failing downstream service holds open threads/connections in the caller. Without a circuit breaker, thread pool exhaustion cascades upstream — the entire call chain fails. Circuit breakers break the cascade by failing fast immediately, freeing resources.

**Key parameters:**
- `failureThreshold` — failures before opening (e.g., 5)
- `successThreshold` — successes in half-open needed to close (e.g., 2)
- `timeout` — how long to wait before entering half-open (e.g., 30s)

**Production implementations:** Netflix Hystrix (original, now maintenance-mode), Resilience4j (current JVM standard), Spring Cloud Circuit Breaker, Istio/Envoy (mesh-level, no code changes).

## Evidence & Examples

Three-state implementation using `AtomicReference<State>` for thread safety:
```java
public <T> T execute(Supplier<T> operation) throws CircuitBreakerOpenException {
    State current = state.get();
    if (current == State.OPEN) {
        if (timeoutElapsed()) { state.compareAndSet(OPEN, HALF_OPEN); current = HALF_OPEN; }
        else throw new CircuitBreakerOpenException("failing fast");
    }
    try { T result = operation.get(); onSuccess(current); return result; }
    catch (Exception e) { onFailure(current); throw e; }
}
```

Usage: open after 5 failures, require 2 successes to close, wait 30s before retrying:
```java
this.circuitBreaker = new CircuitBreaker(5, 2, Duration.ofSeconds(30));
return circuitBreaker.execute(() -> callPaymentGateway(request));
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/proxy-pattern]] — API gateways and service meshes incorporate circuit breaking as a first-class infrastructure feature
- [[wiki/concepts/saga-pattern]] — circuit breakers protect individual saga steps from propagating failures through the whole saga
- [[wiki/concepts/loose-coupling]] — circuit breakers enforce temporal decoupling: downstream failure does not freeze the upstream caller
- [[wiki/concepts/messaging-integration]] — async messaging naturally achieves circuit-breaker resilience by design; synchronous RPC calls (RPI) need explicit circuit breakers

## Contradictions
None across current sources.

## Sources
- [[wiki/sources/design-patterns-reimagined]] — comprehensive Java implementation of all three states, failure/success counting, and PaymentService usage example
