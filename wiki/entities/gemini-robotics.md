---
date: 2026-04-15
type: entity
name: Gemini Robotics
aliases: [Gemini Robotics-ER, Gemini Robotics-ER 1.6]
tags: [ai, robotics, physical-ai, embodied-reasoning, google-deepmind]
sources: 1
---

# Gemini Robotics

**Type:** product
**Also known as:** Gemini Robotics-ER, Gemini Robotics-ER 1.6

## Overview

Gemini Robotics is Google DeepMind's family of foundation models designed specifically for robotics applications. The current generation is Gemini Robotics-ER 1.6, where "ER" stands for Embodied Reasoning. Unlike general-purpose vision-language models, Gemini Robotics-ER is optimized for physical-world interpretation: spatial relationship understanding, multi-camera view synthesis, task success detection, and analog instrument reading.

Its first major commercial deployment is within Boston Dynamics' Orbit/AIVI platform, where it powers visual inspection for the Spot robot in industrial environments.

## Key Facts

- Current version: Gemini Robotics-ER 1.6 (ER = Embodied Reasoning) [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Built by Google DeepMind; integrated with Google Cloud infrastructure [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Core capabilities:
  - **Spatial reasoning**: understanding relationships between objects across a scene [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
  - **Multi-camera synthesis**: combining views from multiple cameras to build a coherent scene understanding [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
  - **Success detection**: determining whether a task was actually completed successfully [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
  - **Instrument reading**: interpreting analog gauges, thermometers, and sight glasses visually [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Deployed in Boston Dynamics' AIVI-Learning system as of April 2026 [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Updates delivered via cloud (zero-downtime upgrades — no robot redeployment needed) [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]

## Connections

- [[wiki/entities/google-deepmind]] — developer
- [[wiki/entities/boston-dynamics]] — first major commercial deployment partner
- [[wiki/entities/spot-robot]] — the robot it currently powers
- [[wiki/concepts/embodied-reasoning]] — the capability this model is built around
- [[wiki/concepts/physical-ai]] — Gemini Robotics is the foundation-model layer in a deployed Physical AI system

## Open Questions

- How does Gemini Robotics-ER 1.6 compare to other vision-language-action (VLA) models?
- What is the model's failure mode profile across diverse industrial environments?
- Is instrument reading general enough to handle non-standard or worn/damaged gauge faces?

## Sources

- [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]] — ER 1.6 capabilities announced alongside Boston Dynamics integration; embodied reasoning framing introduced
