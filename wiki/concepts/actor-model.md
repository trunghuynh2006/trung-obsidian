---
date: 2026-04-22
type: concept
name: Actor Model
aliases: [Actor Model Pattern, Actors, Akka, Erlang Actor Model, Virtual Actors]
tags: [software-architecture, design-patterns, concurrency, distributed-systems, messaging]
sources: 1
---

# Actor Model

## Definition
A concurrency model in which the fundamental unit of computation is an **actor** — an independent entity with private state, a mailbox queue, and behavior defined by how it processes incoming messages. Actors communicate exclusively through asynchronous message passing, eliminating shared mutable state and the need for locks.

## Detail

**Core properties:**
- Each actor has **private state** — no other actor can read or write it directly; no getter calls, no shared references.
- Each actor processes messages **sequentially** from its mailbox — at most one message at a time. Its own state is never accessed concurrently; no locks needed.
- Actors communicate exclusively via **immutable messages** sent asynchronously to mailboxes.
- The **actor system** manages lifecycle (creation, supervision, termination), thread allocation, and message dispatch.

**Why it eliminates classic concurrency bugs:** Traditional shared-memory concurrency requires locks, which introduce deadlocks, livelocks, and race conditions. The Actor Model makes these impossible by design: no memory is shared, only messages are exchanged. The actor's sequential message processing is the implicit lock.

**Scalability:** Multiple actors run concurrently on different threads or machines because they share no state. Distributed actor systems (Erlang/OTP, Akka Cluster) allow actors to span machines transparently — the same message-passing interface works whether the target actor is local or remote.

**Supervision trees:** Erlang/OTP and Akka support actor supervision — parent actors define restart strategies for their children on failure, enabling fine-grained fault isolation without crashing the whole system.

**Production frameworks:** Akka (JVM), Erlang/OTP (Erlang/Elixir — the original), Microsoft Orleans (.NET), Ray (Python/distributed ML), Pony.

**Constituents:**
- Actor — private state + mailbox + `receive(message)` dispatch logic
- Mailbox — bounded queue of pending messages (oldest first)
- Messages — immutable data structures
- Actor system — thread pool, message routing, lifecycle management, supervision

## Evidence & Examples

BankAccount as an actor — no lock needed because `balance` is only accessed inside `receive()`, which is called for one message at a time:
```java
public class BankAccountActor extends Actor {
    private BigDecimal balance;  // private; never accessed outside receive()
    protected void receive(Message message) {
        if (message instanceof DepositMessage dm)
            balance = balance.add(dm.getAmount());
        else if (message instanceof TransferMessage tm)
            handleTransfer(tm);  // sends DepositMessage to target actor
    }
}
```

No lock, no synchronized block, no AtomicReference — thread safety comes from message serialization.
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/backpressure]] — actor mailboxes need backpressure strategies when producers are faster than the actor can consume
- [[wiki/concepts/observer-pattern]] — actors communicate via messages analogously to observers receiving update calls, but with no shared method invocation
- [[wiki/concepts/saga-pattern]] — saga orchestrators are a natural fit for the actor model: stateful, long-running, message-driven
- [[wiki/concepts/async-await]] — actor `receive` loops are conceptually related to async event handlers; Kotlin coroutines and actors share the same scheduler
- [[wiki/concepts/messaging-integration]] — the Actor Model is the in-process analog of async messaging integration; Erlang actors inspired many message broker designs
- [[wiki/concepts/exbodied-intelligence]] — the RAnts swarm robots follow an analogous architecture: independent agents, private local state, stimulus-response behavior — actor-model principles at the hardware level

## Sources
- [[wiki/sources/design-patterns-reimagined]] — BankAccountActor, ActorSystem with thread pool and actor registry; thread-safe balance management without a single lock
