---
type: concept
name: Edge AI
aliases: [on-device AI, edge inference, TinyML]
tags: [ai, iot, edge-computing, hardware, architecture]
sources: 1
---

# Edge AI

## Definition

The deployment of AI models directly on end devices — sensors, microcontrollers, edge gateways — rather than in centralized cloud or backend systems. Processing happens at the point of data collection, with little or no dependency on network connectivity.

## Why It Matters

The naive IoT architecture sends all raw sensor data to a central server for processing. Edge AI inverts this: intelligence lives on the device. The consequences are significant:

- **Latency:** decisions in milliseconds, not round-trip seconds
- **Bandwidth:** transmit only meaningful events, not continuous raw streams
- **Reliability:** operates during network outages
- **Privacy/sovereignty:** sensitive data never leaves the device or facility

## Model Optimization Techniques

Running neural networks on resource-constrained hardware requires aggressive optimization:

- **Quantization** — reduce weight precision from 32-bit floats to 8-bit integers (or less); 4× memory reduction with minimal accuracy loss
- **Pruning** — remove low-weight connections from a trained network; reduces computation with modest accuracy tradeoff
- **Knowledge distillation** — train a small "student" model to mimic a large "teacher" model; captures essential capabilities at a fraction of the size
- **Purpose-built edge AI chips** — silicon specifically designed for neural network inference at milliwatt power levels; enables battery-powered sensors to run continuous inference for years

[[wiki/sources/the-intelligent-edge-how-ai-and-large]]

## Federated Learning at the Edge

Edge AI nodes can train collaboratively without sharing raw data. Each node trains locally and shares only model weight *updates*; a coordinator aggregates these into a global model. This enables:

- Privacy preservation (raw sensor data stays local)
- Bandwidth efficiency (weight deltas vs. raw data streams)
- Collective learning (entire network benefits from each node's experience)

See [[wiki/concepts/federated-learning]] for full treatment.

## The Edge-Cloud Continuum

Edge AI is not all-or-nothing. A hybrid architecture is common:

1. **Edge node** — lightweight model handles routine cases locally
2. **Edge gateway/device** — more powerful; handles complex local processing, aggregates across multiple nodes
3. **Cloud/backend** — receives only summarized data and exception events; handles long-horizon analysis, model retraining, and fleet-wide coordination

When edge devices encounter scenarios beyond their local model's capability, they escalate to more powerful cloud resources while maintaining overall system responsiveness. [[wiki/sources/the-intelligent-edge-how-ai-and-large]]

## LLMs at the Edge

Smaller, distilled LLMs are now deployable on edge devices, enabling:
- Natural language queries against local sensor data
- Conversational maintenance interfaces for technicians
- Decision explanations in plain English without cloud roundtrips

This is particularly significant for industrial settings where connectivity is unreliable or where latency requirements preclude cloud calls.

## Connections

- [[wiki/concepts/federated-learning]] — the distributed training complement to edge inference
- [[wiki/concepts/industrial-iot]] — the primary deployment context for industrial edge AI
- [[wiki/concepts/predictive-maintenance]] — the killer application; local inference on vibration/thermal data
- [[wiki/concepts/physical-ai]] — edge AI is the cognitive layer for AI-powered physical systems
- [[wiki/concepts/robot-components]] — edge AI runs on the "control system" component; enhanced sensor nodes are sensors with an embedded control system

## Sources

- [[wiki/sources/the-intelligent-edge-how-ai-and-large]] — comprehensive treatment of edge AI architecture, optimization techniques, and industrial applications
