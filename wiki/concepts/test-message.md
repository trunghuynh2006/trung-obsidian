---
date: 2026-04-18
type: concept
name: Test Message
aliases: [synthetic transaction, canary message]
tags: [enterprise-integration, messaging, patterns, monitoring]
sources: 1
---

# Test Message

## Definition

A message with known inputs and expected outputs, injected into a live message stream to verify that a service is returning correct results — not just responding, but responding accurately.

## Detail

**The limitation of availability monitoring:** Knowing that a service is responding (no timeout) does not mean it is returning correct results. A malfunctioning service may return a technically valid response with wrong data (e.g., a credit-scoring service that returns 0 for every customer, causing all orders to be rejected).

**How Test Messages work:**
1. A **Test Data Generator** periodically injects a request message for a known subject (a person whose credit score is known in advance).
2. The Test Message includes a special [[wiki/concepts/return-address]] pointing to a separate test reply channel.
3. A **Test Data Verifier** monitors the test reply channel and checks not just that a reply arrived, but that the content is correct.
4. The [[wiki/concepts/smart-proxy]] handles routing: it separates test reply traffic from production reply traffic using the Return Address mechanism.

**Statistical complement:** Test Messages detect discrete correctness failures. A complementary approach is statistical sampling: if a service declines >5 orders in a row, flag for human review. Test Messages and statistical sampling together provide coverage that neither alone can achieve.

**Non-intrusiveness concern:** Test Messages consume service capacity (and in the case of paid external services, may incur charges). Keep injection frequency low and use the Smart Proxy to separate test traffic from production billing.

## Evidence & Examples

- WGRUS: external credit agency is a paid service with a QoS contract. A Smart Proxy wraps it; a Test Data Generator periodically injects test requests. The Test Data Verifier checks replies on a separate channel via Return Address routing [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/smart-proxy]] — required to separate test reply channels from production reply channels
- [[wiki/concepts/return-address]] — the mechanism that routes test replies to the verifier, not the production consumer
- [[wiki/concepts/control-bus]] — test results and alerts are published here for the management console
- [[wiki/concepts/wire-tap]] — simpler monitoring: copies messages passively vs. Test Message's active correctness verification

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS testing and monitoring section for verifying the external credit agency
