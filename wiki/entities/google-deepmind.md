---
date: 2026-04-15
type: entity
name: Google DeepMind
aliases: [DeepMind, GDM]
tags: [ai, robotics, physical-ai, frontier-ai]
sources: 1
---

# Google DeepMind

**Type:** org
**Also known as:** DeepMind, GDM

## Overview

Google DeepMind is Alphabet's primary AI research and development organization, formed in 2023 by merging Google Brain and DeepMind. It is responsible for foundational AI research (AlphaGo, AlphaFold, Gemini) and increasingly for frontier model deployment across products and partners.

In robotics, DeepMind has developed the Gemini Robotics model family — foundation models designed specifically for physical-world reasoning and manipulation. Their framing centers on "embodied reasoning": not just perceiving the world visually, but interpreting spatial relationships, understanding task context, and determining whether actions have succeeded.

## Key Facts

- Developed Gemini Robotics-ER 1.6, a model purpose-built for robotics embodied reasoning [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Introduced "embodied reasoning" as a capability framing: spatial analysis, multi-camera synthesis, success detection, instrument reading [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]
- Partnered with Boston Dynamics to integrate Gemini Robotics-ER 1.6 into Spot's Orbit/AIVI platform (2026) [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]]

## Connections

- [[wiki/entities/boston-dynamics]] — robotics deployment partner for Gemini Robotics
- [[wiki/entities/gemini-robotics]] — their robotics-specific model family
- [[wiki/entities/anthropic]] — frontier AI peer; both now active in physical/embodied AI, though via different paths
- [[wiki/entities/openai]] — frontier AI peer
- [[wiki/concepts/embodied-reasoning]] — the capability framing DeepMind is centering its robotics work around
- [[wiki/concepts/physical-ai]] — Gemini Robotics is DeepMind's entry into foundation-model-powered Physical AI

## Open Questions

- How does Gemini Robotics-ER 1.6 compare architecturally to other vision-language-action models (e.g., RT-2, OpenVLA)?
- What is DeepMind's longer-term commercial model for robotics — platform licensing, API-per-query, or hardware bundling?

## Sources

- [[wiki/sources/boston-dynamics-integrates-google-deepminds-gemini-robotics-model-into-spot-inspection-platform]] — Gemini Robotics-ER 1.6 release; embodied reasoning capabilities; Boston Dynamics partnership
