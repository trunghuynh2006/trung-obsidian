---
type: concept
name: Robot Components
aliases: [robot hardware, robot anatomy]
tags: [robotics, hardware, components, reference]
sources: 1
---

# Robot Components

## Definition

The four fundamental hardware subsystems present in most robots: sensors (input), actuators (output/motion), control system (processing), and power supply (energy).

## Components

### Sensors — The Eyes and Ears
Gather information from the environment:
- **Vision sensors** — capture visual data (cameras, depth sensors)
- **Proximity sensors** — detect nearby objects
- **Range sensors** — measure distances (ultrasonic, LIDAR)
- **Force sensors** — measure applied force / contact

Related concept: perception is one of robotics' hardest unsolved problems [[wiki/concepts/robotics-multidisciplinarity]].

### Actuators — The Muscles
Convert energy into motion:
- **Electric motors** — controlled rotational or linear movement (most common in hobby/research)
- **Pneumatic actuators** — use compressed air; fast but less precise
- **Hydraulic actuators** — use pressurized fluid; high force output

### Control Systems — The Brain
Central processing:
- **Microcontrollers** — execute instructions (e.g. Arduino for beginners [[wiki/entities/arduino]])
- **Single-board computers** — more powerful; run OS (e.g. Raspberry Pi, Jetson Nano)
- **Software / algorithms** — control loops, planning, perception pipelines
- **Communication interfaces** — connect subsystems and external devices

### Power Supply — The Fuel
- **Batteries** — portable; the standard for mobile robots
- **AC/DC converters** — for stationary or tethered systems
- **Power transformers** — regulate voltage to different subsystems

## AI-Enhanced Sensor and Actor Nodes

The IoT world uses "sensor nodes" and "actor nodes" — these map directly onto the sensors and actuators taxonomy, but with embedded intelligence added:

- **AI-enhanced sensor node** = sensor + edge AI control system co-located on one device. Rather than transmitting raw data, it runs local inference (e.g., vibration pattern recognition for bearing wear) and transmits only meaningful events. [[wiki/concepts/edge-ai]]
- **AI-enhanced actor node** = actuator + reasoning layer. Goes beyond executing commands to *explaining* decisions, adapting behavior, and coordinating with other actor nodes. Example: smart irrigation system that explains in natural language why it's watering a specific zone. [[wiki/concepts/industrial-iot]]

This is the same four-component taxonomy operating at higher cognitive density per node: the control system component now runs neural networks alongside classical control loops.

## Connections

- [[wiki/entities/arduino]] — a microcontroller; the beginner-level control system component.
- [[wiki/concepts/robotics-multidisciplinarity]] — each component maps to a discipline (sensors→perception, actuators→ME/EE, control→CS/EE, power→EE).
- [[wiki/concepts/robotics-simulation]] — simulation abstracts hardware components; lets you focus on control/software before physical components are wired.
- [[wiki/concepts/edge-ai]] — AI-enhanced sensor nodes embed the control system and edge AI chip into a single unit.
- [[wiki/concepts/industrial-iot]] — IIoT sensor and actor nodes are the deployed form of AI-enhanced robot components.

## Sources

- [[wiki/sources/robotics-for-beginners-playtolabs]] — defines the four-component taxonomy.
- [[wiki/sources/the-intelligent-edge-how-ai-and-large]] — AI-enhanced sensor/actor nodes as intelligent extensions of the sensor/actuator model.
