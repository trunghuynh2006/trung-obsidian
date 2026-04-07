---
type: concept
name: Federated Learning
aliases: [federated ML, distributed learning]
tags: [ai, ml, privacy, iot, distributed-systems]
sources: 1
---

# Federated Learning

## Definition

A distributed machine learning approach where multiple nodes train models locally on their own data and share only model weight *updates* — never raw data — with a central coordinator. The coordinator aggregates updates into a global model, which is then redistributed to all nodes.

## How It Works

1. Central coordinator distributes a base model to all nodes
2. Each node trains on its local data, producing updated weights
3. Nodes send weight *deltas* (not data) to the coordinator
4. Coordinator aggregates (typically by weighted averaging) into a new global model
5. Updated global model is pushed back to all nodes
6. Repeat

## Why It Matters for IoT

In sensor networks, raw data is often:
- **Private** — industrial production data, patient readings, proprietary process data
- **Voluminous** — continuous sensor streams that would overwhelm network bandwidth if transmitted
- **Locally correlated** — a sensor's data is most relevant in the context of nearby sensors

Federated learning solves all three problems simultaneously: the network improves collectively without any node's raw data leaving its local environment. [[wiki/sources/the-intelligent-edge-how-ai-and-large]]

## Trade-offs

- **Communication overhead:** weight updates are smaller than raw data but still require periodic synchronization
- **Non-IID data problem:** nodes may have locally biased data distributions; the global model must generalize across all of them
- **Convergence speed:** slower than centralized training on pooled data
- **Byzantine robustness:** a compromised node could inject adversarial weight updates

## Connections

- [[wiki/concepts/edge-ai]] — federated learning is the training mechanism that improves edge AI models over time
- [[wiki/concepts/industrial-iot]] — industrial sensor networks are a primary use case; keeps proprietary process data on-premises
- [[wiki/concepts/predictive-maintenance]] — fleets of industrial sensors can collectively improve failure prediction models without sharing raw readings

## Sources

- [[wiki/sources/the-intelligent-edge-how-ai-and-large]] — introduces federated learning in the IoT sensor network context; emphasis on privacy and bandwidth advantages
