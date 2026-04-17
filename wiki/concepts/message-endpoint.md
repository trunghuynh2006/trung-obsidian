---
date: 2026-04-18
type: concept
name: Message Endpoint
aliases: [Channel Adapter, Messaging Gateway, endpoint]
tags: [enterprise-integration, messaging, patterns]
sources: 1
---

# Message Endpoint

## Definition

A component that connects an application to a messaging channel, translating between the application's internal API/event model and the messaging infrastructure.

## Detail

Most legacy, packaged, and even many custom applications were not designed to participate in a messaging system. A Message Endpoint is the adapter that bridges the gap. Without it, the application cannot send or receive messages.

**Two common endpoint variants:**

### Channel Adapter
Connects to an application externally — the application may not even be aware of the adapter. Typical strategies:
- **Database trigger adapter**: adds triggers to specific tables; fires a message when a row is inserted/updated.
- **API poller**: periodically calls the app's API and publishes changes as messages.
- Bidirectional: can also consume messages and invoke actions inside the application.

*When to use:* Packaged or legacy applications with no integration hooks. You cannot change the app.

WGRUS: the call center system (packaged app) is connected via a Channel Adapter on its database. The inbound fax Access database is similarly connected.

### Messaging Gateway
Code embedded inside a custom application that isolates the application's business logic from messaging-specific code. The application calls the gateway via a clean API; the gateway handles serialization, channel selection, and delivery.

*When to use:* Custom-built applications where you control the source code. Keeps application code clean.

WGRUS: the custom J2EE web application uses a Messaging Gateway to publish orders, so the web code never directly references the messaging infrastructure.

## Connections

- [[wiki/concepts/message-channel]] — the channel the endpoint connects the app to
- [[wiki/concepts/message-translator]] — often paired with an endpoint to transform formats
- [[wiki/concepts/smart-proxy]] — enhances a basic endpoint/service with additional capability

## Sources

- [[wiki/sources/enterprise-integration-patterns-ch1]] — Channel Adapter and Messaging Gateway introduced in WGRUS order-taking design
