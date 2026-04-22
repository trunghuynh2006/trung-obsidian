---
date: 2026-04-22
type: concept
name: Flyweight Pattern
aliases: [Flyweight]
tags: [software-architecture, design-patterns, structural, optimization, oop]
sources: 1
---

# Flyweight Pattern

## Definition
A structural pattern (Gang of Four, 1994) that minimizes memory usage by sharing data among similar objects. De-emphasized or removed from modern pattern catalogs as premature optimization.

## Detail
Flyweight was designed for applications that create large numbers of similar fine-grained objects — characters in a text editor, trees in a 3D scene — where individual instantiation was too memory-intensive. The pattern separates **intrinsic state** (shared, immutable, stored in the flyweight) from **extrinsic state** (passed in by the caller at use time), and manages shared object pools.

The problem today: **premature optimization**. Modern hardware has abundant memory, and the complexity Flyweight adds — careful intrinsic/extrinsic state separation, pool management, coordinated access — is rarely justified. When memory optimization is genuinely needed, better tools exist: string interning (language-level), object pooling libraries, memory-efficient data structures (bit arrays, off-heap storage), and arena allocators.

The Flyweight principle survives implicitly in language features: Java string interning, enum singletons, and value-type semantics (Java 21 value classes, Kotlin data classes) implement the same idea without hand-coded patterns.

## Connections
- [[wiki/concepts/singleton-pattern]] — Flyweight's shared instance pool uses a similar global-access mechanism
- [[wiki/concepts/actor-model]] — Actor systems achieve high concurrency and low per-entity overhead via message passing rather than memory sharing

## Sources
- [[wiki/sources/design-patterns-reimagined]] — identifies Flyweight as a premature-optimization pattern whose complexity is no longer justified by modern hardware
