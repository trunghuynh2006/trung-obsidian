---
date: 2026-04-22
type: concept
name: Abstract Factory Pattern
aliases: [Abstract Factory]
tags: [software-architecture, design-patterns, creational, oop]
sources: 1
---

# Abstract Factory Pattern

## Definition
A creational pattern (Gang of Four, 1994) that provides an interface for creating families of related objects without specifying their concrete classes. Considered over-engineered and obsolete in most modern codebases.

## Detail
Abstract Factory was designed for scenarios where a system must create groups of compatible objects — the canonical example being UI widgets that all belong to the same look-and-feel theme (Windows, Mac). The pattern requires a deep hierarchy: abstract factory interface → concrete factory implementations → abstract product interfaces → concrete product implementations. This parallel structure is difficult to understand, extend, and maintain.

Modern dependency injection frameworks handle the same problem more elegantly: the framework is configured to use the appropriate concrete implementations at startup, and components receive their dependencies via injection. The elaborate parallel class hierarchies are avoided entirely.

The pattern has niche legitimacy in environments without DI frameworks, but in the mainstream is a candidate for simplification.

## Evidence & Examples

Classic structure (three levels of abstraction — verbose and rigid):
```java
public interface GUIFactory { Button createButton(); Checkbox createCheckbox(); }
public class WindowsFactory implements GUIFactory {
    public Button createButton() { return new WindowsButton(); }
    public Checkbox createCheckbox() { return new WindowsCheckbox(); }
}
// + MacFactory + WindowsButton + MacButton + WindowsCheckbox + MacCheckbox
```

Modern replacement: DI container configured at startup; components inject `Button` (interface) and receive the right implementation automatically.
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/singleton-pattern]] — the other GoF creational pattern flagged for removal from the modern catalog
- [[wiki/concepts/loose-coupling]] — Abstract Factory solves a coupling problem but over-engineers the solution
- [[wiki/concepts/strategy-pattern]] — Strategy's functional transformation is the simpler modern analog for varying behavior families

## Sources
- [[wiki/sources/design-patterns-reimagined]] — identifies Abstract Factory as over-engineered for DI-based environments; simpler alternatives preferred
