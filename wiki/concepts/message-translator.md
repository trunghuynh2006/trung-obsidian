---
date: 2026-04-18
type: concept
name: Message Translator
aliases: [transformer, data mapper]
tags: [enterprise-integration, messaging, patterns, transformation]
sources: 1
---

# Message Translator

## Definition

A component that converts a message from one application's data format into another's, sitting between a channel adapter/endpoint and the downstream channel.

## Detail

Integration developers rarely control the internal data formats of the applications they connect. A Message Translator sits between systems and converts formats so each application can stay in its own schema while the integration layer handles the mapping.

**Key design decisions:**
- Translators are placed at the boundary of each application — once at the source (convert from app-specific to canonical), once at the target (convert from canonical to app-specific).
- This means each message is translated twice, but the payoff is that adding a new source or target system only requires one new translator, not N×M translators.
- Hand-coding translators is tedious and error-prone; prefer declarative mapping tools when available.

**Naming convention (WGRUS):** Application-specific channels are named with the app prefix (`WEB_NEW_ORDER`); canonical channels are named after the message intent (`NEW_ORDER`). The translator bridges the two.

**Why use it even for your own app?** WGRUS uses a translator for the web interface even though they control its code. Reason: shields the downstream canonical flow from future format changes in the web app. The cost is one extra translation; the benefit is isolation.

## Evidence & Examples

- WGRUS: three translators convert call center, web, and fax order formats → canonical `NEW_ORDER` format [[wiki/sources/enterprise-integration-patterns-ch1]]
- WGRUS: separate translators for widget vs. gadget inventory systems, because each uses a different internal format [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/canonical-data-model]] — defines the target format that all translators map to/from
- [[wiki/concepts/message-endpoint]] — typically paired: endpoint connects to app; translator converts format
- [[wiki/concepts/message-channel]] — translator sits between the app-specific channel and the canonical channel

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS order intake and inventory routing designs
