---
date: 2026-04-07
type: concept
name: Robot Types
aliases: [robot taxonomy, types of robots, robot categories]
tags: [robotics, taxonomy, reference]
sources: 2
---

# Robot Types

## Definition

A taxonomy of robots organized by form factor, application domain, or movement style. Different types require different skill emphases — an industrial robot demands control and mechanical precision; an autonomous mobile robot demands perception and planning.

## Taxonomy (by application)

| Type | Description | Common Domains |
|---|---|---|
| **Humanoid** | Human-like appearance and behavior | Research, customer service |
| **Cobot** | Collaborative robot; works safely alongside humans | Manufacturing, assembly |
| **Domestic** | Household tasks (cleaning, cooking, laundry) | Consumer |
| **Hospital** | Surgery assistance, medication delivery, patient transport | Healthcare |
| **Medical** | Surgery, medication, rehabilitation therapy | Healthcare |
| **Industrial** | Repetitive manufacturing tasks (welding, painting) | Manufacturing |
| **Articulated** | Multiple joints for multidirectional movement | Manufacturing, assembly |
| **Cartesian** | Linear X/Y/Z axis movement | Assembly, packaging, 3D printing |
| **Autonomous Mobile (AMR)** | Independent navigation for delivery, security, exploration | Logistics, security |
| **Disaster Response** | Search-and-rescue, damage assessment | Emergency services |
| **Entertainment** | Theme parks, museums, home | Consumer, hospitality |

## Notes

- Hospital and Medical are listed separately in the source but overlap significantly in practice.
- Cobot (collaborative robot) is a design philosophy as much as a type — emphasizes human-safe operation.
- AMRs are among the fastest-growing segments driven by logistics automation.

## 2026 Status Updates

**Humanoids:** Technology is finally catching up with the hype. China has set national targets for mass production; Hyundai announced plans to deploy humanoids across global operations. Mainstream industrial deployment is now on a visible timeline. [[wiki/sources/robotics-trends-2026]]

**Cobots:** ISO 10218 and ANSI/A3 R15.06 (2025) dropped the term "collaborative robot" — replaced by "collaborative application." Safety is now defined at the application level, not by robot type. Cobots are more popular than ever and are proliferating via **Robots-as-a-Service (RaaS)**, bringing automation within reach of SMBs. [[wiki/sources/robotics-trends-2026]]

**Industrial robots:** Not made obsolete by cobots — rather, cobots have joined the portfolio. Industrial robots are also becoming more collaboratively deployed. Both categories coexist and are growing.

## Connections

- [[wiki/concepts/robotics-multidisciplinarity]] — each type emphasizes different disciplines (AMR → perception/planning; industrial → control/mechanics; medical → precision/safety).
- [[wiki/concepts/robotics-career-paths]] — career roles align to robot types (e.g. field service technician → industrial; research scientist → humanoid/AMR).
- [[wiki/concepts/physical-ai]] — Physical AI is being layered onto humanoids and AMRs first; transforming what these types can do.

## Sources

- [[wiki/sources/robotics-for-beginners-playtolabs]] — defines the 11-type taxonomy.
- [[wiki/sources/robotics-trends-2026]] — 2026 status updates for humanoids, cobots, and industrial robots.
