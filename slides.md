---
theme: seriph
title: Securing Robotics in Practice
info: |
  ## Securing Robotics in Practice
  Developer Workflows, Architecture, and the ROS2 Ecosystem
class: text-center
drawings:
  persist: false
transition: slide-left
comark: true
duration: 7min
monaco: false
mdc: true
---

# Securing Robotics in Practice
## Developer Workflows, Architecture, and the ROS2 Ecosystem

Patrick Robinson  
patrick2.robinson@live.uwe.ac.uk

<div class="pt-8 text-lg opacity-80">
A short talk on security, architecture, and real-world robotics practice
</div>

<!--
Open simply.

Suggested opening:
"As robotics systems move into real-world deployment, ensuring their security becomes increasingly important. But in practice, securing robotics systems is surprisingly difficult."
-->

---
transition: slide-left
layout: center
---

# The core claim

<div class="text-3xl leading-snug max-w-4xl mx-auto pt-6">
In robotics, security is often shaped not just by <span class="font-bold">bugs in code</span>,
but by <span class="font-bold">how systems are assembled</span>.
</div>

<div class="grid grid-cols-3 gap-8 pt-12 text-left max-w-5xl mx-auto">
<div>
<h3 class="pb-2">Workflows</h3>
<ul>
<li>rapid integration</li>
<li>toolchain churn</li>
<li>time and resource constraints</li>
</ul>
</div>
<div>
<h3 class="pb-2">Architecture</h3>
<ul>
<li>distributed nodes</li>
<li>heterogeneous components</li>
<li>networked communication</li>
</ul>
</div>
<div>
<h3 class="pb-2">Context</h3>
<ul>
<li>research vs industry</li>
<li>different risk tolerances</li>
<li>different compliance pressures</li>
</ul>
</div>
</div>

<!--
This slide states the argument plainly.
Do not over-explain yet.
End with: "So the question is not just whether a component is secure, but how security is produced across the system."
-->

---
transition: slide-left
---

# A typical robotics system

<div class="text-lg leading-7 pr-4">
This is a deliberately simplified example, but it captures the shape of many modern robotics systems:

- sensors, perception, planning, control
- extra components added over time
- operator and cloud-facing interfaces
- communication over ROS2 / DDS

<div class="pt-4 font-semibold">
Even a "normal" setup is already distributed, heterogeneous, and interconnected.
</div>
</div>

<!--
Walk left to right.

Suggested script:
"You have sensors feeding perception, then planning, then control, which ultimately drives behaviour. But these systems are not self-contained. They often include third-party nodes, operator interfaces, and external services, all connected through middleware like ROS2 using DDS."
-->

---
transition: none
---
# A typical robotics system

<div class="text-lg leading-7 pr-4">

```mermaid {theme: 'neutral', scale: 0.6}
flowchart LR
  S[Sensors] --> P[Perception Node]
  P --> PL[Planning Node]
  PL --> C[Control Node]
  C --> A[Actuators]

  TP[Third-party Node] --> P
  UI[Operator UI] <--> PL
  CL[Cloud Service] <--> TP

  ROS2[(ROS2 / DDS)]
  P --- ROS2
  PL --- ROS2
  C --- ROS2
  TP --- ROS2
```

<div class="pt-4 font-semibold">
 - 
</div>

</div>

---
transition: slide-up
---
# A typical robotics system

<div class="text-lg leading-7 pr-4">

```mermaid {theme: 'neutral', scale: 0.6}
flowchart LR
  S[Sensors] --> P[Perception Node]
  P --> PL[Planning Node]
  PL --> C[Control Node]
  C --> A[Actuators]

  TP[Third-party Node] --> P
  UI[Operator UI] <--> PL
  CL[Cloud Service] <--> TP

  ROS2[(ROS2 / DDS)]
  P --- ROS2
  PL --- ROS2
  C --- ROS2
  TP --- ROS2
```

<div class="pt-4 font-semibold">
Even a "normal" setup is already distributed, heterogeneous, and interconnected.
</div>

</div>


---
transition: slide-left
layout: two-cols
layoutClass: gap-10
---

# Where does security actually live?

<div class="text-lg leading-7 pr-4">
Imagine a new component is added quickly:

- open-source package
- vendor-supplied module
- code from another internal team

<div class="pt-4">
The system may still <span class="font-semibold">work</span> — but security questions now sit across configuration, middleware, trust assumptions, and interfaces between components.
</div>

<div class="pt-6 text-2xl font-semibold">
Not in one place — across the system.
</div>
</div>

::right::

```mermaid {theme: 'neutral', scale: 0.9}
flowchart LR
  S[Sensors] --> P[Perception Node]
  P --> PL[Planning Node]
  PL --> C[Control Node]
  C --> A[Actuators]

  TP["New / third-party node"] --> P
  UI[Operator UI] <--> PL
  CL[Cloud Service] <--> TP

  ROS2[(ROS2 / DDS)]
  P --- ROS2
  PL --- ROS2
  C --- ROS2
  TP --- ROS2

  classDef risk fill:#fbe4e6,stroke:#cc3344,stroke-width:2px,color:#111;
  class TP risk;
```

<div class="absolute bottom-12 right-12 w-[34%] text-base bg-white/70 dark:bg-black/20 p-3 rounded">
<ul>
<li>Who can publish data?</li>
<li>What assumptions are trusted?</li>
<li>What happens when behaviour changes?</li>
</ul>
</div>

<!--
Suggested script:
"Now imagine we integrate a new component quickly to meet a deadline. The robot still works. But who authenticates that node? What assumptions does it make about the network? What happens if it publishes unexpected data? At that point, security is not located in one file or one bug. It is distributed across the way the system has been assembled."
-->

---
transition: slide-left
layout: two-cols
layoutClass: gap-12
---

# So what is the research?

<div class="text-lg leading-7">
I am studying how security is approached <span class="font-semibold">in practice</span> across diverse robotics contexts.

<div class="pt-4"></div>

### Empirical strand
- surveys
- semi-structured interviews
- sampling across research, commercial, and industrial settings

### Analytical strand
- how standards and frameworks define system boundaries
- what counts as a "robotic system"
- how those assumptions shape security thinking
</div>

::right::

```mermaid {theme: 'neutral', scale: 0.95}
flowchart TD
  A[Different robotics contexts] --> B[Workflows and tools]
  A --> C[Architectural decisions]
  A --> D[Security priorities]
  E[Standards / frameworks] --> C
  E --> D
  B --> F[Observed practices]
  C --> F
  D --> F
  F --> G[Practical security interventions]
```

<div class="pt-4 text-base opacity-80">
The aim is not a single universal account, but a better map of how security is produced under different conditions.
</div>

<!--
This is where you briefly acknowledge diversity and instability without becoming too philosophical.
If needed say: "Part of the work is also about how these systems are framed and categorised in the first place, because those categories affect who we recruit, what we ask, and what counts as security-relevant." 
-->

---
transition: slide-left
layout: center
---

# Why this matters

<div class="grid grid-cols-3 gap-8 text-left max-w-5xl mx-auto pt-8">
<div>
<h3 class="pb-2">For research</h3>
<ul>
<li>moves beyond isolated vulnerabilities</li>
<li>connects security to architecture and practice</li>
<li>helps map a fragmented space</li>
</ul>
</div>
<div>
<h3 class="pb-2">For practitioners</h3>
<ul>
<li>surfaces real friction points</li>
<li>fits security to existing workflows</li>
<li>avoids unrealistic assumptions</li>
</ul>
</div>
<div>
<h3 class="pb-2">For robotics</h3>
<ul>
<li>supports safer deployment</li>
<li>better design-stage reasoning</li>
<li>more robust system integration</li>
</ul>
</div>
</div>

<div class="pt-10 text-2xl font-semibold max-w-4xl mx-auto">
If we want secure robots in the real world, we need to understand how security is actually made in the systems people build.
</div>

<!--
Slow down here. This is the payoff slide.
-->

---
transition: slide-left
layout: center
class: text-center
---

# Thank you

<div class="text-2xl pt-6">
I would love to hear from people who build or deploy robotics systems.
</div>

<div class="pt-8 text-lg opacity-85">
Especially if you have experience with:
</div>

<div class="pt-4 text-xl">
security · integration · architecture · ROS2 workflows
</div>

<div class="pt-12">
patrick2.robinson@live.uwe.ac.uk
</div>

<!--
Possible close:
"At this stage, I am especially interested in speaking to people who have run into security, integration, or architectural challenges in practice."
-->

