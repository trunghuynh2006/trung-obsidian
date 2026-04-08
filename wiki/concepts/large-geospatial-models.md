---
type: concept
name: Large Geospatial Models
aliases: [LGM, geospatial world models]
tags: [geospatial, robotics, physical-ai, spatial-computing]
sources: 1
---

# Large Geospatial Models

## Definition

Shared, machine-readable spatial representations of the physical world that let AI systems and robots localize themselves, interpret environments, and operate against a common map of real space. In the current source set, the term is used in a practical deployment sense rather than as a purely theoretical AI architecture.

## Detail

The Niantic Spatial source frames Large Geospatial Models as the missing substrate for physical-world AI. The core argument is that many real environments remain opaque to machines because they are not mapped in forms useful for robotics: 3D reconstructions, meshes, Gaussian splats, and localization-ready visual landmarks.

This concept adds an important nuance to [[wiki/concepts/physical-ai]]. Real-world AI systems need more than perception, planning, and control. They also need shared spatial grounding: a persistent representation of the environments they act within. In the source's framing, environment capture tools such as Scaniverse and localization systems such as VPS are complementary pieces of that substrate.

## Evidence & Examples

- Niantic Spatial explicitly describes Scaniverse and VPS 2.0 as part of a broader "Large Geospatial Model" effort [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- Scaniverse produces 3D environment assets that can be used to train and deploy robotics and AI systems [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]
- VPS 2.0 provides localization inside those environments, especially where GPS is unreliable [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]

## Connections

- [[wiki/concepts/physical-ai]] — large geospatial models provide spatial grounding for physical AI deployment
- [[wiki/concepts/visual-positioning-systems]] — VPS is one operational layer of a large geospatial model
- [[wiki/entities/niantic-spatial]] — introduces the term in this wiki's current source set
- [[wiki/entities/coco-robotics]] — example deployment showing why shared geospatial understanding matters for mobile robots

## Contradictions

None yet in the current source set.

## Sources

- [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]] — introduces the concept and ties it to Scaniverse + VPS infrastructure
