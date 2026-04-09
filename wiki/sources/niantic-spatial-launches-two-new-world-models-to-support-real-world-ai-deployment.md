---
date: 2026-04-08
type: source
title: "Niantic Spatial launches two new world models to support real-world AI deployment"
source_file: raw/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment.md
date_ingested: 2026-04-08
tags: [physical-ai, geospatial, robotics, localization, spatial-computing]
---

# Niantic Spatial launches two new world models to support real-world AI deployment

**Source:** [[raw/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment.md]]
**Ingested:** 2026-04-08
**Tags:** #physical-ai #geospatial #robotics #localization #spatial-computing

## Summary

This source argues that a major bottleneck in real-world AI is not model intelligence alone, but the absence of accurate, machine-readable representations of physical space. Niantic Spatial positions its new products, **Scaniverse for businesses** and **VPS 2.0**, as infrastructure for closing that gap: one captures environments as shareable 3D assets, the other localizes machines inside those environments using camera input rather than GPS.

The article is most useful to this wiki as a refinement of [[wiki/concepts/physical-ai]]. It adds a missing deployment layer between simulation and operation: robots and other physical AI systems need not only reasoning and control, but also reliable spatial grounding. Scaniverse provides the mapping substrate; VPS provides the localization substrate; together they support what Niantic calls a **Large Geospatial Model** — a shared spatial understanding for machines.

The robotics angle is concrete rather than speculative. Niantic says its SDK will support [[wiki/entities/ros2]], and delivery robotics company [[wiki/entities/coco-robotics]] is cited as an existing user of the visual positioning stack. The broader claim is that industries such as construction, energy, logistics, manufacturing, and the public sector remain hard for AI to penetrate until this spatial-data layer becomes easier to build and deploy.

## Key Points

- **Spatial data as the bottleneck:** Niantic argues that physical-world AI is constrained by missing machine-readable maps, not just by intelligence limits.
- **Scaniverse for businesses:** captures rooms through industrial sites using smartphones or 360-degree cameras, producing meshes and Gaussian splats for robotics and AI workflows.
- **Collaborative mapping:** multiple users can contribute scans into a single cloud-hosted environment model.
- **Consumer-device capture:** the system is explicitly framed as avoiding specialized scanning hardware.
- **VPS 2.0:** uses camera input and computer vision for localization, especially where GPS is weak or unavailable.
- **Tiered localization:** VPS 2.0 can operate globally at a basic level, then switch to higher-precision localization in mapped areas.
- **Large Geospatial Model framing:** Niantic presents these tools as pieces of a shared spatial-understanding layer for machines.
- **Robotics deployment signal:** [[wiki/entities/coco-robotics]] is named as a live user, and SDK 4.0 support is planned for Unity, Swift, Android, and [[wiki/entities/ros2]].

## Connections

- [[wiki/entities/niantic-spatial]] — company building the mapping and localization stack described here
- [[wiki/entities/coco-robotics]] — cited deployment example for VPS-enabled autonomous navigation
- [[wiki/entities/ros2]] — named as a supported SDK target, linking the stack into mainstream robotics tooling
- [[wiki/concepts/physical-ai]] — source adds spatial grounding as missing infrastructure for real-world deployment
- [[wiki/concepts/large-geospatial-models]] — this source introduces the term and its role as shared machine understanding of space
- [[wiki/concepts/visual-positioning-systems]] — VPS 2.0 is the article's concrete localization mechanism

## Quotes

> "the lack of accurate, machine-readable maps of the physical world"

> "near centimeter-level" accuracy in mapped environments

> "progress in physical-world applications depends less on advances in intelligence and more on access to reliable spatial data"
