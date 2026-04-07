### This is what getting Started in Robotics Really Looks Like.

I get this question a lot.  
“How do I get started in robotics?”

I don’t always have a clean answer. Not because I’m hiding anything. But because the question itself is messy.

[AskRobotics](https://www.reddit.com/r/AskRobotics/) on reddit is proof of that. Every time someone asks it, you’ll see dozens of conflicting replies. And the questions doesn’t keep coming every month. Learn ROS2 first. No, learn C++. Start with electronics. No, start with math. Buy a robot kit. No, start in simulation.

This write-up exists to clear the fog.

The reality is simple. Robotics looks mature from the outside, but under the hood, we’re still early even if you see many cool dancing videos of humanoids.

Robotics still has hard, unsolved problems. Perception in the real world and dealing with uncertainities. Reliable manipulation and grasping irregular shaped objects, Energy-efficient actuation, Robust autonomy outside controlled environments to mention but a few. Many ideas that look great in papers remain lab demos or simulations because real life is messy and unforgiving.

That gap between research, prototype, and product is where most beginners get confused.

## Why There’s No Single Entry Point

Robotics is multidisciplinary by nature. That’s the core issue.

Mechanical design. Electronics. Embedded systems. Control. Software. Perception. AI. Systems integration. You can spend years in just one of these and still feel behind.

That’s why giving a single “start here” answer is almost impossible.

Before anything else, two questions matter more than any roadmap:

- How old are you and what level of education are you at?
- What do you already know?

The mistake beginners make is trying to master everything upfront. CAD. PCBs. Control theory. C++. ROS. Machine learning.

That approach guarantees burnout.

Early on, you don’t need depth. You need just enough skill to make something move, sense, or react. Learning should follow the problem you’re trying to solve, not an abstract checklist.

Pure robotics degrees are still rare. In the U.S., fewer than 100 universities offer a dedicated bachelor’s degree in robotics out of thousands. Most roboticists arrive through adjacent fields.

That’s normal. That’s how the field works.

## The Myth of the “Perfect Roboticist”

People love imagining the ideal background.

Electrical engineering. Mechanical engineering. Computer science. A master’s in data science. Another master’s in robotics. Maybe a PhD. Plus internships.

That’s more than a decade of study. It’s not realistic. And it’s not how real roboticists are made.

Robotics isn’t about knowing everything. It’s about knowing **how systems fail**, and how to learn what you need when they do.

## If You’re in High School

If you’re young, curiosity is your unfair advantage.

The best shortcut here is competition teams like [FIRST Robotics,](https://www.firstinspires.org/) [VEX](https://www.vexrobotics.com/?srsltid=AfmBOoootWNPqVYk0HP5HFamzz_iAHE5bE8BYmJVYn88BjKonlr_53hG), [RoboFest](https://www.robofest.net/) etc Any environment where you’re forced to build, break, and iterate with deadlines. Join a robotics summer camp or maybe attend a local library events and use their 3d printers.

If competitions aren’t accessible, a basic mobile robot kit is enough. Arduino. DC motors. Ultrasonic sensors. Line following. Obstacle avoidance.

Program it. Modify it. Add sensors. Make it do something slightly smarter than before.

If you’re still excited after that, you’re on the right path.

From there, you can add encoders. Learn basic feedback control. Play with PID without overthinking the math. Try different motors. Add a camera. Do simple vision tasks.

Eventually, you’ll hit the limits of a microcontroller Arduino board. That’s expected.

That’s when single-board computers come in. Raspberry Pi. Jetson Nano. Or even a laptop taped to the robot. Ugly is fine. Function comes first.

You can redesign the platform. Learn basic CAD. 3D print parts. Iterate again.

If you reach university still excited after all this, congratulations.

## If You’re in University

If your school has a robotics program, great. If not, pick a core discipline and borrow from the others.

Mechanical engineering with CS and EE electives.  
Electrical engineering with ME and CS electives.  
Computer science with systems, math, and hardware exposure.

There’s no wrong entry point. There’s only incomplete ones.

What matters is staying hands-on.

## Why Roadmaps Don’t Work

Everyone wants a roadmap. I understand why. Roadmaps feel safe.

But most robotics roadmaps are useless.

They confuse **order** with **learning**.

Learning robotics isn’t linear. You don’t finish electronics before touching ROS. You don’t master kinematics before opening a simulator. You loop. You revisit concepts. You learn just enough to unblock yourself. That is why I created a skill tree which will vary across job roles and robot type.

![](https://substackcdn.com/image/fetch/$s_!HkUf!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F56c4485c-635d-4618-aee2-18f5673a297c_1500x2000.png)

I’ve seen students waste months trying to “complete” roadmaps instead of building anything real. They stall. They overprepare. They quit.

Good roboticists don’t follow roadmaps. They follow problems.

“My robot drifts.”  
“My localization breaks.”  
“My grasp fails.”

Each problem creates its own learning path. That path is personal. No diagram can predict it.

Build something. Break it. Fix it. Document it. Repeat.

That’s the real roadmap.

## Graduate School and Advanced Degrees

Many people enter robotics through graduate school. Usually from ME, EE, CS, physics, or math backgrounds.

Graduate robotics is less about building full robots and more about solving specific problems. Control. Perception. Planning. Learning. Hardware subsystems.

Core courses usually include:

- Kinematics and dynamics
- Estimation and control
- Perception and sensing
- Planning and navigation

Advanced courses go deeper into topics like legged locomotion, reinforcement learning, Human-robot interaction, Medical robotics, Soft robotics, Multi-robot systems etc

These programs are math-heavy with topics like Linear algebra, Probability, Optimization and Calculus. You can’t escape that.

A PhD is different. Coursework is a fraction. Most learning is self-directed. Your advisor matters more than the syllabus. Thus, you have to choose carefully.

A PhD trains you to answer questions no one has answered before. That’s the job and not to deploy robots in the field.

[Robohub](https://robohub.org/) has a publication on “Careers in robotics: Should you get a PhD or go into industry?” written by Professor [Sonia Roberts](https://www.linkedin.com/in/sonia-roberts-1bba7aa/). You can read it [here](https://robohub.org/careers-in-robotics-should-you-get-a-phd-or-go-into-industry/).

## Practical Action Points

Most robotics roles expect a college degree. That’s the baseline reality.

If you haven’t started:

- Get a STEM bachelor’s degree
- Join hands-on clubs
- Build projects
- Join a robotics club or Robotics competition
- Apply for internships

If your degree is unrelated:

- Identify math and technical gaps
- Fill them deliberately
- Be honest about your limits
- Get hands-on without rushing hardware

Simulation helps. A lot.

- No setup headaches
- Faster iteration
- Cheap or free

Start small. Move a robot. Avoid an obstacle. Follow a line. Pick up a block.

Then add complexity slowly.

Overambitious projects kill momentum.

And document everything. Your portfolio matters more than certificates.

## Final Thought

Robotics isn’t something you “finish learning.”

It’s something you grow into by staying curious longer than most people are comfortable with.

Build first. Learn as needed. Repeat.

That’s how real roboticists are made.

---

On the topic of Robotics roles and what to expect in them, check out [Akshet Patel blogpost](https://akshetpatel.substack.com/p/10-robotics-roles-and-what-to-expect) on this. And thanks to Akshet Patel for providing initial feedback on the first draft. Subscribe to his newsletter [here](https://substack.com/@akshetpatel)

On the topic of getting a robotics job, here ([Part 1](https://medium.com/@ardalantj/how-to-become-a-robotics-engineer-d7a9678fc1f8) and [Part 2](https://medium.com/@ardalantj/how-to-become-a-robotics-engineer-part-2-2-9bdc3f15f60e)) is a good blog post by [Ardalan Tajbakhsh](https://www.linkedin.com/in/ardalantajbakhsh/)

For links to some robotics online courses or education, check [here](https://docs.google.com/document/d/1wC32Cbc-xNR19mXHkpB5k4gBKUEv0_y11taSPxyMPiw/edit?usp=sharing). it is a growing list I am compiling.

---