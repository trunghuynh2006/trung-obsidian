---
date: 2026-04-07
type: entity
name: Arduino
aliases: []
tags: [product, hardware, microcontroller, robotics, embedded]
sources: 1
---

# Arduino

**Type:** product / hardware platform
**Category:** Microcontroller / embedded systems

## Overview

An open-source microcontroller platform widely used in robotics prototyping and education. Designed for accessibility — low cost, large community, simple programming environment. The canonical starting point for hardware-oriented robotics beginners.

In a beginner robotics path, Arduino typically represents the first hardware platform: connect motors, sensors, and write firmware to make the robot behave. Its limits (processing power, memory, no OS) eventually push learners toward single-board computers (Raspberry Pi, Jetson Nano), which is itself a natural learning milestone.

## Key Facts

- Common beginner project stack: Arduino + DC motors + ultrasonic sensors + line following / obstacle avoidance. [[wiki/sources/robotics-getting-started]]
- Natural upgrade path: Arduino → encoders → PID → camera → single-board computer (Raspberry Pi, Jetson Nano). [[wiki/sources/robotics-getting-started]]
- Hitting Arduino's limits is expected and signals readiness for more powerful platforms.

## Connections

- [[wiki/concepts/problem-driven-learning]] — Arduino projects are a natural problem-driven learning loop: add a sensor, try to make it work, hit limits, upgrade.
- [[wiki/entities/first-robotics]] — competition teams often use more capable controllers, but Arduino is the at-home equivalent starting point.

## Sources

- [[wiki/sources/robotics-getting-started]] — recommended as the first hardware platform for high school beginners.
