---
date: 2026-04-18
type: concept
name: Canonical Data Model
aliases: [CDM, canonical format, common message format]
tags: [enterprise-integration, messaging, patterns, transformation]
sources: 1
---

# Canonical Data Model

## Definition

A single, application-independent message format agreed upon by all participants in an integration solution, so that each application only needs one translator (to/from canonical) rather than a translator for every pair of applications.

## Detail

**The N×M problem:** Without a canonical model, connecting N applications requires up to N×(N-1) translators (one for each directed pair). With a canonical model, you need at most 2×N translators (one into canonical, one out of canonical, per application).

**Two message categories** (from WGRUS):
- **Canonical (public) messages**: defined in the canonical model; travel on shared channels; can be consumed by any component. Named after business intent: `NEW_ORDER`, `VALIDATED_ORDER`, `ADDRESS_CHANGE`.
- **Application-specific (private) messages**: defined by individual apps; travel on app-prefixed channels; should only be consumed by the app and its associated translator. Named with app prefix: `WEB_NEW_ORDER`, `WIDGET_INV_CHECK`.

**Design tradeoff:** The canonical model is only as stable as its design. If the shared format changes (e.g., you add a currency field), all translators must be updated. Getting the canonical model right up front matters.

**Practical note:** Canonical model design is partly a political exercise — it often becomes the center of inter-team negotiation about whose semantics win ("whose definition of 'account' do we use?").

## Evidence & Examples

- WGRUS uses a canonical `NEW_ORDER` format; three translators (web, call center, fax) all produce it; downstream consumers (inventory, billing, shipping) all consume it [[wiki/sources/enterprise-integration-patterns-ch1]]
- Adding a new order channel (e.g., email ordering) would only require one new translator, not changes to inventory/billing/shipping [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/message-translator]] — the component that performs canonical ↔ app-specific conversion
- [[wiki/concepts/enterprise-application-integration]] — canonical data model solves the N×M problem in multi-app integration
- [[wiki/concepts/message]] — canonical messages are the public messages in the canonical model

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS order intake design; public/private channel naming convention
