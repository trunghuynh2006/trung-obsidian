---
date: 2026-05-08
type: entity
name: Raspberry Pi
aliases: [RPi, Pi]
tags: [product, hardware, single-board-computer, robotics, embedded, linux]
sources: 0
---

# Raspberry Pi

**Type:** product / hardware platform
**Category:** Single-board computer (SBC)

## Overview

A credit-card-sized single-board computer running Linux (Raspberry Pi OS). Designed for education and prototyping, it has become the canonical platform for robot builds that outgrow Arduino's processing limits. Unlike Arduino, the Pi runs a full OS, supports Python natively, and can handle tasks requiring networking, computer vision, and AI inference.

The natural upgrade path in beginner robotics is Arduino → Raspberry Pi: once you need a camera, vision processing, ROS2, or edge AI, Arduino's limited RAM and lack of OS become blockers. The Pi resolves all three.

## Key Facts

- Main variants: Pi 4 (4GB/8GB RAM, good all-rounder), Pi 5 (faster, best for vision/AI), Pi Zero 2W (lightweight, wireless, constrained).
- GPIO pins (40-pin header) allow direct sensor and actuator control, analogous to Arduino digital pins.
- Primary language: Python (via `RPi.GPIO`, `gpiozero`, or `pigpio` libraries).
- Motor control on Pi typically uses a dedicated motor HAT or driver board (e.g., Adafruit Motor HAT, L298N via GPIO).
- Camera: Pi Camera Module or USB webcam; OpenCV is the standard vision library.
- Can run [[wiki/entities/ros2]] natively — the standard path for ROS2 development on affordable hardware.
- Supports edge AI inference: TensorFlow Lite, PyTorch Mobile, ONNX Runtime.

## Connections

- [[wiki/entities/arduino]] — the typical hardware predecessor; Pi replaces Arduino when vision, networking, or OS features are needed.
- [[wiki/entities/ros2]] — Raspberry Pi is the standard affordable hardware platform for running ROS2.
- [[wiki/concepts/edge-ai]] — Pi (especially Pi 5 with NPU) can run quantized models locally for on-robot inference.
- [[wiki/concepts/physical-ai]] — Pi-based robots are a practical stepping stone toward production Physical AI systems.
- [[wiki/concepts/problem-driven-learning]] — hitting Arduino limits is the natural trigger for learning the Pi; the upgrade itself is problem-driven.
- [[wiki/analyses/ultralearning-for-raspberry-pi]] — full 6-week study plan applying Scott Young's nine ultralearning principles to Raspberry Pi robot building.
- [[wiki/analyses/ultralearning-for-arduino-robot]] — the prerequisite path; skills built on Arduino transfer directly to Pi GPIO and motor control.
