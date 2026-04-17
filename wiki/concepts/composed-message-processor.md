---
date: 2026-04-18
type: concept
name: Composed Message Processor
aliases: [CMP]
tags: [enterprise-integration, messaging, patterns, routing]
sources: 1
---

# Composed Message Processor

## Definition

A named composite pattern that combines a Splitter, a Content-Based Router, and an Aggregator to process individual parts of a composite message independently and then recombine the results.

## Detail

The Composed Message Processor is not a new primitive — it is a named shorthand for a very common three-step pipeline:

```
Composite Message
      ↓
  [Splitter]  — breaks into N individual messages
      ↓
[Content-Based Router]  — routes each to the correct handler
      ↓
 [Handlers]  — process each item independently
      ↓
  [Aggregator]  — recombines N results into one
      ↓
Result Message
```

**Why give it a name?** Because this pipeline appears so frequently in integration design that teams need a single symbol for it in architecture diagrams. The name allows architects to say "use a Composed Message Processor here" rather than re-explaining the three-step construction every time.

**Encapsulation value:** Individual handlers (e.g., inventory systems) can still be composed of multiple internal steps, wired via their own message flows or orchestrated by a nested Process Manager. The CMP pattern applies recursively.

## Evidence & Examples

- WGRUS multi-item order inventory check: the Splitter breaks the order into items → CBR routes each item to widget or gadget inventory → Aggregator recombines results [[wiki/sources/enterprise-integration-patterns-ch1]]
- The book explicitly introduces the CMP symbol to replace the expanded Splitter+Router+Aggregator diagram in the WGRUS architecture pictures [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/splitter]] — first component in the pipeline
- [[wiki/concepts/content-based-router]] — middle component
- [[wiki/concepts/aggregator]] — final component
- [[wiki/concepts/process-manager]] — alternative for more complex orchestration with explicit state management

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — defined in WGRUS multi-item order processing section
