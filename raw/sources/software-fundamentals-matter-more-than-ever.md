fIn this talk, Matt Pocock argues that software engineering fundamentals are more important than ever in the age of AI. He warns against the "specs-to-code" movement, noting that relying solely on AI to generate code from specifications leads to software entropy—a state where the codebase becomes progressively worse and harder to change (0:34-4:15).

He outlines several failure modes of AI-assisted development and provides solutions based on time-tested principles:

Aligning on the "Design Concept": To avoid building the wrong thing, use a "grill me" technique (5:50-7:20) where you have the AI interview you until a shared understanding is reached.
Establishing a Ubiquitous Language: To prevent verbosity and misalignment, create a shared vocabulary with the AI in a markdown file, rooted in Domain-Driven Design principles (8:13-9:42).
Leveraging TDD and Feedback Loops: AI often struggles with taking small, deliberate steps. Using Test-Driven Development (TDD) forces the AI to operate within tight feedback loops, which acts as a speed limit to prevent bugs (10:23-11:32).
Implementing Deep Modules: Avoid "shallow modules" (tiny, complex blobs). Instead, structure your architecture into deep modules with simple interfaces, which makes the code easier to test and allows the AI to focus on implementation while you design the strategic boundaries (12:43-14:50).
Managing Cognitive Load: Treat deep modules as "gray boxes" where you control the interface and delegate the implementation to the AI, which saves your mental energy (15:26-16:26).
Matt concludes that while AI is an excellent "tactical programmer," the human developer must act as the strategic architect, constantly investing in the system's design (17:23-18:02).