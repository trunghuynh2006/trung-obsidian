---
date: 2026-04-22
type: concept
name: Async-Await Pattern
aliases: [Async/Await, Async Await, CompletableFuture, Coroutines, Futures]
tags: [software-architecture, design-patterns, concurrency, reactive, async]
sources: 1
---

# Async-Await Pattern

## Definition
A concurrency pattern that allows asynchronous code to be written in a sequential, top-to-bottom style while still executing non-blocking operations. Not in the original GoF catalog; now fundamental to modern application development across nearly every language.

## Detail

**The problem it solves — callback hell:** Before async-await, multi-step async workflows required deeply nested callbacks. Each step required passing a success callback and an error callback into the prior step. Error handling was scattered; the control flow was inside-out; the code width grew with every step.

**The pattern:** Mark a function as `async`; use `await` inside it to pause execution until an asynchronous operation completes. When `await` is encountered, the function suspends and returns control to the caller — the thread is freed for other work. When the awaited operation completes, execution resumes from the suspension point. Error handling uses familiar try/catch semantics.

**Language support:**
- **Python** — native `async def` / `await`, `asyncio.gather()` for concurrent execution
- **JavaScript/TypeScript** — native `async`/`await` over Promises
- **C#** — native `async`/`await` over Tasks (since C# 5)
- **Kotlin** — coroutines (`suspend`, `launch`/`async`/`withContext`)
- **Java** — `CompletableFuture` chains (`thenCompose`, `thenApply`, `allOf`) — verbose but equivalent; virtual threads (Java 21+, Project Loom) let blocking-style code run with non-blocking throughput

**Concurrent execution of independent operations:**
```python
# Run inventory check and credit check concurrently rather than sequentially
inventory_task = inventory_service.check_inventory(order.items)
credit_task = credit_service.check_credit(order.customer_id, order.total)
inventory, credit = await asyncio.gather(inventory_task, credit_task)
```

**Constituents:**
- Async functions — contain `await` expressions; return futures/promises/tasks
- Await expressions — suspend function execution; yield thread; resume on completion
- Event loop / task scheduler — manages queued async work
- Promise/Future/Task — the underlying value representing an eventual result

## Evidence & Examples

Python async-await (sequential-style, clean error handling):
```python
async def process_order(order_id):
    order = await order_service.get_order(order_id)
    inventory = await inventory_service.check_inventory(order.items)
    if not inventory.is_available():
        raise Exception("Inventory not available")
    payment = await payment_service.process_payment(order.payment)
    shipment = await shipping_service.create_shipment(order)
    return OrderResult(order, shipment)
```

vs. Java callback hell (same logic — deeply nested, hard to follow):
```java
orderService.getOrder(orderId, new Callback<Order>() {
    public void onSuccess(Order order) {
        inventoryService.checkInventory(order.getItems(), new Callback<InventoryResult>() {
            public void onSuccess(InventoryResult inv) {
                paymentService.processPayment(order.getPayment(), new Callback<PaymentResult>() {
                    // ... one more level
                });
            }
        });
    }
});
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/backpressure]] — async-await handles individual futures; backpressure is needed when async operations produce continuous streams of items
- [[wiki/concepts/actor-model]] — actor message processing is an async receive loop; conceptually related but at a coarser granularity
- [[wiki/concepts/saga-pattern]] — saga steps are typically implemented as async operations awaited in sequence

## Sources
- [[wiki/sources/design-patterns-reimagined]] — Java callback hell vs. CompletableFuture vs. Python native async-await; concurrent execution with asyncio.gather()
