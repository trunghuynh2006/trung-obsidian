---
date: 2026-04-18
type: concept
name: Smart Proxy
aliases: [service proxy, message proxy]
tags: [enterprise-integration, messaging, patterns, monitoring, orchestration]
sources: 1
---

# Smart Proxy

## Definition

A component that intercepts both request and reply messages to and from a service, transparently adding capabilities (Return Address support, quality-of-service tracking, response-time measurement) without modifying the service itself.

## Detail

**The problem:** Legacy services cannot be changed to support [[wiki/concepts/return-address]] or to emit metrics. You still need those capabilities for the system to participate in a Service-Oriented Architecture or to be monitored.

**How it works:**
1. **Intercept the request**: replace the caller's Return Address with a fixed internal reply channel; store the original Return Address internally.
2. **Forward to the service**: the service sends its reply to the fixed internal channel.
3. **Intercept the reply**: read the reply, retrieve the stored original Return Address, forward the reply to the caller's channel. Optionally record metrics (response time, errors).

**Two main uses in WGRUS:**

### Use 1: Enabling Return Address on a legacy service
The Smart Proxy stores the original Return Address from the caller and re-routes the service's reply to the correct channel. The legacy service never knows about the caller's reply address — it always replies to the proxy's fixed channel.

### Use 2: Quality-of-Service tracking
The Smart Proxy timestamps requests and replies to measure response times. It publishes metrics to the [[wiki/concepts/control-bus]] for the management console. If no reply arrives within a timeout, it reports a failure.

**Non-intrusive:** The service and the caller are unaware of the proxy. The proxy is transparent middleware.

## Evidence & Examples

- WGRUS SOA: Smart Proxy wraps legacy inventory/billing/shipping systems to add Return Address support without changing those systems [[wiki/sources/enterprise-integration-patterns-ch1]]
- WGRUS testing/monitoring: Smart Proxy wraps the external credit agency service to track request/reply timing and report to the Control Bus; also supports injecting Test Messages [[wiki/sources/enterprise-integration-patterns-ch1]]

## Connections

- [[wiki/concepts/return-address]] — the capability Smart Proxy adds to legacy services
- [[wiki/concepts/control-bus]] — destination for metrics and QoS data collected by the Smart Proxy
- [[wiki/concepts/wire-tap]] — simpler: passive copy of messages; Smart Proxy actively intercepts and modifies routing
- [[wiki/concepts/test-message]] — Smart Proxy enables Test Messages by separating test reply channels from production reply channels

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — introduced in WGRUS SOA design and testing/monitoring section; two distinct use cases
