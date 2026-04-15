---
date: 2026-04-15
type: entity
name: Boston Dynamics
aliases: [BD]
tags: [robotics, physical-ai, industrial-inspection]
sources: 1
---

# Boston Dynamics

**Type:** org
**Also known as:** BD

## Overview

Boston Dynamics is a robotics company known for developing highly capable mobile robots, most notably Spot (a quadruped inspection robot) and Atlas (a humanoid). Originally spun out of MIT in 1992 and later acquired by Hyundai Motor Group (2021), the company has shifted in recent years from research demonstrations toward commercial industrial deployment.

Their software platform, Orbit, serves as the operational brain for Spot deployments — handling mission scheduling, data management, and increasingly AI-powered visual analysis through the AI Visual Inspection (AIVI) and AIVI-Learning systems.

## Key Facts

- Developed Spot, a quadruped robot widely deployed for industrial inspection [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Orbit software platform: manages Spot missions, captures visual data, hosts AIVI/AIVI-Learning [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Partnered with Google Cloud and Google DeepMind to integrate Gemini Robotics-ER 1.6 into AIVI (2026) [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Data-sharing model: customer inspection data is used to train/adapt AI models but stays within Boston Dynamics, not shared with Google [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]

## Connections

- [[wiki/entities/spot-robot]] — their flagship commercial robot
- [[wiki/entities/google-deepmind]] — AI partner for Gemini Robotics integration
- [[wiki/entities/gemini-robotics]] — the AI model integrated into their platform
- [[wiki/concepts/physical-ai]] — Boston Dynamics' current commercial direction is a concrete instance of foundation-model-powered Physical AI
- [[wiki/concepts/embodied-reasoning]] — the capability Boston Dynamics is adding to Spot via Gemini Robotics-ER 1.6
- [[wiki/concepts/predictive-maintenance]] — instrument reading and equipment monitoring are the industrial application

## Open Questions

- How does Boston Dynamics' data-sharing model (customer data stays with BD, not Google) affect model improvement rates relative to federated or fully cloud-shared approaches?
- What reliability floor do Gemini Robotics-ER reasoning capabilities hit in highly unpredictable industrial environments (extreme dust, lighting variability, unusual configurations)?

## Sources

- [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]] — Gemini Robotics-ER integration into Spot's AIVI platform; detection → reasoning transition
