---
type: concept
name: Predictive Maintenance
aliases: [PdM, condition-based maintenance, CBM]
tags: [industrial-iot, ai, manufacturing, reliability]
sources: 1
---

# Predictive Maintenance

## Definition

A maintenance strategy that uses continuous sensor monitoring and AI analysis to predict equipment failures *before* they occur — enabling maintenance to be scheduled proactively rather than performed reactively after breakdown or on a fixed calendar interval.

## The Three Maintenance Paradigms

| Paradigm | Trigger | Cost profile |
|---|---|---|
| **Reactive** | Equipment fails | High: unplanned downtime, emergency repair |
| **Preventive** | Fixed schedule | Medium: planned downtime, some unnecessary work |
| **Predictive** | Sensor-detected degradation | Low: minimal downtime, work only when needed |

Predictive maintenance shifts the curve from the first two to the third by making equipment health continuously visible. [[wiki/sources/the-intelligent-edge-how-ai-and-large]]

## Signal Types Used

AI models analyze multiple sensor modalities to detect degradation signatures:

- **Vibration analysis** — bearing wear, misalignment, imbalance appear as characteristic frequency components in accelerometer data
- **Thermal imaging** — hot spots indicate friction, electrical faults, or insulation failure
- **Acoustic emissions** — ultrasonic signatures of crack propagation, cavitation, or lubrication loss
- **Current/power draw** — motor degradation changes electrical load profiles

A steel manufacturing plant example: sensor networks monitor critical machinery; AI schedules maintenance during planned production downtime, avoiding unplanned outages that could halt production for days. [[wiki/sources/the-intelligent-edge-how-ai-and-large]]

## LLM Integration

LLMs add two capabilities on top of raw anomaly detection:

1. **Explanation** — translate detected anomaly patterns into natural-language diagnoses ("bearing wear in pump #3, likely due to misalignment; recommend replacement within 2 weeks")
2. **Query interface** — maintenance engineers ask "Which machines need attention this week?" rather than manually reviewing dashboards; LLM synthesizes sensor data into prioritized recommendations

This democratizes access: plant operators without deep signal processing expertise can act on complex sensor analysis.

## Edge vs. Backend Architecture

- **Edge deployment** — sensor-local inference for immediate alerts (e.g., vibration threshold crossed → local alarm); no cloud dependency
- **Backend deployment** — long-horizon trend analysis across historical data; correlation across entire fleets; model retraining

The two layers complement each other. Edge provides real-time response; backend provides the pattern library that makes edge models accurate. [[wiki/concepts/edge-ai]]

## Connections

- [[wiki/concepts/edge-ai]] — predictive maintenance is edge AI's primary industrial killer app; local inference on vibration/thermal data
- [[wiki/concepts/industrial-iot]] — the deployment context; predictive maintenance is IIoT's highest-value use case
- [[wiki/concepts/federated-learning]] — fleets of industrial sensors can improve shared failure prediction models without sharing raw data
- [[wiki/concepts/physical-ai]] — predictive maintenance is one way AI integrates with physical systems at the infrastructure level

## Sources

- [[wiki/sources/the-intelligent-edge-how-ai-and-large]] — describes predictive maintenance in steel manufacturing and industrial pump contexts; covers sensor modalities, AI analysis, and LLM query interfaces
