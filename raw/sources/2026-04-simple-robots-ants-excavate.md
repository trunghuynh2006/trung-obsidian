![Simple robots inspired by ants collectively build and excavate](https://scx1.b-cdn.net/csz/news/800a/2026/simple-robots-inspired.jpg)

An illustration of how the collective, decentralized behavior of ants has inspired experiments with cooperative robots that can complete tasks without central control. Credit: Harvard John A. Paulson School of Engineering and Applied Sciences

When it comes to teamwork, we could all learn something from ants. These relatively simple, small-brained animals are famous for their ability to collectively build massive, intricate, climate-controlled structures, despite having neither a blueprint nor a worksite foreman.

Researchers from the Harvard John A. Paulson School of Engineering and Applied Sciences (SEAS) and Faculty of Arts and Sciences, who have [long been fascinated](https://www.quantamagazine.org/does-form-really-shape-function-20250612/) by physical phenomena that orchestrate extraordinarily complex natural processes—from ant colonies, to [brain folds](https://medicalxpress.com/news/2026-01-curiosity-driven-journey-brain.html), to the [human gut](https://phys.org/news/2024-10-gut-genetics-physics-embryonic.html) —have developed a fleet of cooperative robots that, very much like ants, can spontaneously organize to build and dismantle structures. They are governed only by environmental cues and minimal physical rules.

Their study, published in [*PRX Life*](https://journals.aps.org/prxlife/abstract/10.1103/cx3h-bwhc), demonstrates how a decentralized swarm of agents, whether robots or insects, can coordinate to complete tasks without central control, offering insights into both biological systems and future autonomous robotic systems.

![](https://www.youtube.com/watch?v=m7oBdhXiPNQ)

Credit: Harvard John A. Paulson School of Engineering and Applied Sciences

The study was led by Professor L. Mahadevan, whose lab has studied social insect communities for many years, and [previously showed](https://techxplore.com/news/2022-12-physical-intelligence-ants-robots-prison.html) they could mimic ants' excavation and escape prowess using robots.

"Our new study shows how simple, local rules can lead to the emergence of complex task completion that is self-organized and thus robust and adaptive," said Mahadevan, the Lola England de Valpine Professor of Applied Mathematics, Organismic and Evolutionary Biology, and Physics at SEAS and FAS.

"We also introduce the concept of ' [exbodied intelligence](https://techxplore.com/news/2025-01-embodied-ai-reveals-robots-toddlers.html?utm_source=embeddings&utm_medium=related&utm_campaign=internal)," where collective cognition arises not solely from individual agents, but from their ongoing interaction with an evolving environment."

The work could lead to many potential applications, from autonomous construction in hazardous environments, to planetary exploration, to experimental models for studying animal behavior.

## Identifying parameters that produce collective behaviors

In their latest study, the team refined their robotic platform to show both excavation and building performance while, crucially, identifying the key parameters needed to achieve those behaviors.

Social insects like ants and termites build complex structures using a biological technique called [stigmergy](https://phys.org/news/2024-04-secret-termites-giant.html?utm_source=embeddings&utm_medium=related&utm_campaign=internal), in which individuals modify their environments and respond to those modifications.

Ants emit [pheromones](https://phys.org/news/2023-06-ants-specialized-communication-center-social.html?utm_source=embeddings&utm_medium=related&utm_campaign=internal) —like a chemical perfume—from their bodies that fellow ants then respond to. Inspired by this natural cascade, Mahadevan's lab uses robotic ants, a.k.a. RAnts, which respond to "photormones"—light fields as digital stand-ins for pheromone fields.

Each robot senses gradients in the photormone field and leaves behind signals as it moves, creating a feedback loop between robots and their environment. This enables coordination across the swarm.

The agents operate using only a few rules: follow gradients in the photormone signal; pick up and transport building blocks in response to these cues; and deposit materials when signal thresholds are met.

These simple rules nonetheless trigger sophisticated behaviors. Robots spontaneously cluster to form nucleation sites, where structures begin to emerge. These sites arise through a mechanism called trapping instability, in which robots become temporarily confined by the signals they generate. As more robots converge on these locations, construction accelerates, producing organized aggregates of building material.

## Swarms that switch between construction and dismantling

Echoing previous work, the researchers found that the swarm's behavior can be tuned by adjusting two key parameters: cooperation strength, or how strongly robots follow the signal gradient; and deposition rate, or whether robots deposit or remove material. By changing these parameters, the researchers showed that their swarm could switch between construction of new structures, or dismantling of existing ones.

The experiments were accompanied by a theoretical framework that describes how agent density, communication signals, and environmental structure evolve together. The model extends classical biological aggregation theories to account for environments that change dynamically as agents act on them.