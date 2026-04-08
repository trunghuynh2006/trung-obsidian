---
type: concept
name: Visual Positioning Systems
aliases: [VPS, visual localization]
tags: [robotics, localization, computer-vision, geospatial, physical-ai]
sources: 1
---

# Visual Positioning Systems

## Definition

Localization systems that use camera input and computer vision to estimate a device or robot's position and orientation in the physical world, especially in places where GPS is unreliable or unavailable.

## Detail

In the current source set, visual positioning appears as a key enabling layer for real-world AI deployment. Rather than depending entirely on satellite navigation, a VPS compares live camera input against known visual features of an environment to determine where a machine is. This is particularly important indoors, underground, and in dense urban areas where GPS often fails or degrades.

The Niantic Spatial source also adds a two-tier deployment idea: broad basic positioning can work without prior scanning, while higher-precision localization becomes possible once an environment has been mapped. This makes VPS not just a standalone technique, but part of a larger mapping-plus-localization stack.

## Evidence & Examples

- Niantic Spatial's VPS 2.0 uses camera input and computer vision to determine position and orientation [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- The source claims "near centimeter-level" accuracy in mapped environments [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- VPS is described as useful indoors, underground, and in dense urban environments where GPS is unreliable [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- Coco Robotics is cited as a real-world navigation use case [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]

## Connections

- [[wiki/concepts/physical-ai]] — VPS gives physical AI systems reliable spatial localization
- [[wiki/concepts/large-geospatial-models]] — VPS is the localization layer that operates against mapped environments
- [[wiki/entities/niantic-spatial]] — source of the VPS 2.0 example in this wiki
- [[wiki/entities/coco-robotics]] — named deployment example
- [[wiki/entities/ros2]] — robotics toolchain connection through Niantic's planned SDK support

## Contradictions

None yet in the current source set.

## Sources

- [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]] — introduces VPS 2.0 as camera-based localization for physical-world AI
