---
date: 2026-04-07
type: entity
name: ROS 2
aliases: [ROS2, Robot Operating System 2]
tags: [product, software, robotics, middleware, framework]
sources: 2
---

# ROS 2

**Type:** product / software framework
**Category:** Robotics middleware

## Overview

The Robot Operating System 2 — an open-source middleware framework for building robot software. Provides messaging between nodes, hardware abstraction, simulation integration, and a large ecosystem of packages. Industry-standard for research and many commercial robotics applications.

Commonly cited as a "start here" recommendation for robotics beginners, but also commonly disputed — the debate ("learn ROS2 first" vs. "learn C++ first" vs. "start with electronics") is offered as evidence that robotics has no single entry point.

## Key Facts

- Frequently cited on r/AskRobotics as a starting recommendation, alongside conflicting alternatives. [[wiki/sources/robotics-getting-started]]
- Industry-standard middleware for robot software development.
- Best approached after having some grounding in C++/Python and understanding of basic robot concepts — trying to start with ROS2 before those foundations often leads to confusion.
- Niantic Spatial says its upcoming SDK 4.0 will support ROS 2, suggesting visual-positioning and spatial-mapping workflows are being packaged for mainstream robotics stacks. [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]]

## Open Questions

- At what stage in a learner's path does ROS2 become appropriate? (Source doesn't give a clear answer — only notes the debate exists.)

## Connections

- [[wiki/concepts/robotics-multidisciplinarity]] — the "learn ROS2 first" debate is a symptom of robotics having no agreed entry point.
- [[wiki/entities/arduino]] — Arduino is the typical hardware entry point; ROS2 is typically introduced later, once hardware basics and programming are established.
- [[wiki/concepts/visual-positioning-systems]] — Niantic's planned ROS 2 support links camera-based localization into common robotics middleware.
- [[wiki/entities/niantic-spatial]] — provider of the spatial SDK that names ROS 2 as a supported target.

## Sources

- [[wiki/sources/robotics-getting-started]] — mentioned briefly as a contested starting recommendation.
- [[wiki/sources/niantic-spatial-launches-two-new-world-models-to-support-real-world-ai-deployment]] — ROS 2 named as a planned SDK 4.0 support target for spatial AI tooling.
