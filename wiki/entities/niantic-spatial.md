---
type: entity
name: Niantic Spatial
aliases: []
tags: [org, spatial-computing, robotics, ai, geospatial]
sources: 1
---

# Niantic Spatial

**Type:** organization
**Also known as:** none

## Overview

Niantic Spatial appears in this wiki as a company building spatial infrastructure for real-world AI systems. In the current source set, its core claim is that physical AI deployment is blocked less by missing intelligence than by missing machine-readable spatial data: maps, reconstructions, and localization systems that let machines understand where they are and what environment they are operating inside.

Its stack, as described here, combines **Scaniverse for businesses** for 3D environment capture with **VPS 2.0** for visual localization. Niantic frames both as components of a broader **Large Geospatial Model** intended to provide shared spatial understanding for robotics and other physical-world AI applications.

## Key Facts

- Launched Scaniverse for businesses and VPS 2.0 as products for real-world AI deployment [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- Argues that many sectors of the physical economy remain inaccessible to AI because detailed spatial data is missing [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- Says Scaniverse can generate meshes and Gaussian splats from smartphone or 360-camera capture [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- Says VPS 2.0 can provide camera-based localization where GPS is unreliable, with higher precision in mapped environments [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- Plans SDK 4.0 support for Unity, Swift, Android, and ROS 2 [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]

## Timeline

- 2026: Launches Scaniverse for businesses and VPS 2.0; frames them as building blocks for a Large Geospatial Model [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]

## Connections

- [[wiki/entities/coco-robotics]] — cited as an existing user of Niantic's VPS stack for delivery robot navigation
- [[wiki/entities/ros2]] — Niantic says its SDK will support ROS 2, linking the platform into robotics software workflows
- [[wiki/concepts/physical-ai]] — Niantic's products are framed as enabling infrastructure for physical-world AI deployment
- [[wiki/concepts/large-geospatial-models]] — Niantic introduces this term as its broader systems vision
- [[wiki/concepts/visual-positioning-systems]] — VPS 2.0 is Niantic's concrete implementation of visual localization

## Open Questions

- How much of Niantic Spatial's current deployment is production-grade versus platform positioning?
- How broadly adopted are Scaniverse and VPS outside the single example named here?

## Sources

- [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]] — introduces Niantic Spatial's mapping, localization, and large-geospatial-model framing
