---
date: 2026-04-22
type: concept
name: Proxy Pattern
aliases: [Proxy, API Gateway, Service Mesh, Sidecar Proxy]
tags: [software-architecture, design-patterns, structural, distributed-systems, microservices]
sources: 1
---

# Proxy Pattern

## Definition
A structural pattern (Gang of Four, 1994) that provides a surrogate or placeholder for another object to control access to it. In modern distributed systems, evolved into API gateways and service meshes that handle cross-cutting concerns at infrastructure scale.

## Detail

**Classic form:** Three variants — remote proxy (represents an object in a different address space), virtual proxy (lazy initialization), protection proxy (access control). All implement the same interface as the real subject and forward calls, optionally with interception logic.

**Modern transformation:** The forwarding-plus-interception intent now operates at a much higher level:

**API Gateway** — the single entry point to a cluster of microservices. Handles:
- Authentication and authorization
- Rate limiting (per-user, per-endpoint)
- Service discovery (routing to live instances via registry)
- Circuit breaking (fail fast if downstream is down)
- Request/response transformation (protocol or format translation)
- Observability (metrics, distributed tracing, access logging)

Examples: Kong, AWS API Gateway, Nginx, Traefik, Azure API Management.

**Service Mesh** (sidecar proxy model) — a lightweight proxy injected alongside every service instance. The mesh handles all service-to-service concerns (mTLS encryption, retries, circuit breaking, load balancing, distributed tracing) transparently, without code changes in the service itself.

Examples: Istio/Envoy, Linkerd, AWS App Mesh, Consul Connect.

The classic code-level Proxy pattern survives for specific cases: lazy loading of expensive objects, dynamic proxies for AOP (Spring, AspectJ), and mock object generation in testing. But the architecturally significant modern proxies are infrastructure components.

## Evidence & Examples

Modern API gateway proxy — a single `handleRequest` method that authenticates, rate-limits, discovers services, circuit-breaks, and records metrics before forwarding:
```java
public Response handleRequest(Request request) {
    User user = authService.authenticate(request.getAuthToken());
    if (!authService.authorize(user, request.getPath())) return Response.forbidden(...);
    if (!rateLimiter.allowRequest(user.getId())) return Response.tooManyRequests(...);
    ServiceInstance service = serviceRegistry.getInstance(serviceName);
    CircuitBreaker cb = circuitBreakerRegistry.getCircuitBreaker(serviceName);
    if (cb.isOpen()) return Response.serviceUnavailable(...);
    Response response = forwardRequest(service, request);
    metrics.recordRequest(serviceName, response.getStatusCode(), elapsed);
    return response;
}
```
[[wiki/sources/design-patterns-reimagined]]

## Connections
- [[wiki/concepts/circuit-breaker]] — circuit breaking is a core feature of modern API gateways and service meshes
- [[wiki/concepts/loose-coupling]] — proxies enforce the location-coupling dimension of loose coupling (callers do not need to know where the real service is)
- [[wiki/concepts/smart-proxy]] — the EAI Smart Proxy is the messaging-layer analog: intercepts request/reply to add QoS tracking to legacy services
- [[wiki/concepts/enterprise-application-integration]] — the EIP Smart Proxy and modern API Gateway solve the same transparency problem at different layers

## Sources
- [[wiki/sources/design-patterns-reimagined]] — traces Proxy evolution from simple forwarding to full API gateway with auth, rate limiting, discovery, circuit breaking, and observability
