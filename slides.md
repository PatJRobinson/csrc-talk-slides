---
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

<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">

# Securing Robotics in Practice
## Developer Workflows, Architecture, and the ROS2 Ecosystem

Patrick Robinson  
patrick2.robinson@live.uwe.ac.uk

A short talk on security, architecture, and real-world robotics practice
</div>

---
transition: slide-left
layout: default
---

# Why this matters


<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">
<div class="text-xl leading-snug max-w-4xl mx-auto pt-6">
Robotics systems are increasingly deployed in real-world environments

where failures are not just software bugs, but can have  
<span class="font-bold">physical and safety-critical consequences</span>.
</div>

<div class="pt-8 text-lg opacity-90 max-w-3xl mx-auto">
Security here affects safety, reliability, and trust — across research, industry, and commercial systems with very different constraints.
</div>
</div>

---
transition: slide-left
layout: default
---

# The core claim

<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">
<div class="text-xl leading-snug max-w-4xl mx-auto pt-6">
In robotics, security is often shaped not just by <span class="font-bold">bugs in code</span>,
but by <span class="font-bold">how systems are assembled</span>.

<div class="grid grid-cols-3 gap-8 pt-12 text-left max-w-4xl mx-auto">
<div>
<h3 class="pb-2">Workflows</h3>
<ul>
<li>rapid integration</li>
<li>toolchain churn</li>
<li>time constraints</li>
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
<li>different constraints</li>
</ul>
</div>
</div>
</div>
</div>

---
transition: slide-left
---

# A typical robotics system

<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">
<div class="text-lg leading-7 max-w-4xl">

Even in a simplified setup:

- sensors → perception → planning → control
- additional components added over time
- operator interfaces and external services
- communication via ROS2 / DDS

<div class="pt-4 font-semibold">
Already distributed, heterogeneous, and interconnected.
</div>

</div>
</div>

---
transition: slide-left
layout: default
---

# A typical robotics system

<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">

```mermaid {theme: 'neutral', scale: 0.68}
flowchart LR
  S[Sensor]
  P[Perception]
  PL[Planning]
  C[Control]
  A[Actuators]

  S --> P --> PL --> C --> A

  UI[Operator UI] -.-> PL
  TP[3rd-party Node] -.-> P
  CL[Cloud Service] -.-> TP
```

<div class="pt-6 text-lg opacity-80">
Multiple components, interacting across a distributed system
</div>
</div>

---
transition: slide-left
layout: default
---

# Where does security actually live?

<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">

```mermaid {theme: 'neutral', scale: 0.68}
flowchart LR
  S[Sensor]
  P[Perception]
  PL[Planning]
  C[Control]
  A[Actuators]

  S --> P --> PL --> C --> A

  UI[Operator UI] -.-> PL
  TP[3rd-party Node] -.-> P
  CL[Cloud Service] -.-> TP

  classDef risk fill:#fbe4e6,stroke:#cc3344,stroke-width:2px,color:#111;
  class TP risk;
```

<div class="pt-6 text-xl max-w-3xl mx-auto">

• What assumptions are trusted?  

</div>

<div class="pt-6 text-2xl font-semibold">
Not in one place - across the system
</div>
</div>

---
transition: slide-left
layout: default
---

# Why ROS2?

<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">

<div class="text-lg leading-7 max-w-4xl">

ROS2 has become a major ecosystem for robotics development.

It is designed around:

- modularity  
- composability  
- distributed communication  
- rapid integration and prototyping  

<div class="pt-6 font-semibold text-xl">
A useful lens for studying how security is actually produced in practice
</div>

</div>

</div>

---
transition: slide-left
layout: default
---

# The research gap

<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">
<div class="text-xl leading-snug max-w-4xl mx-auto">

We still have only a <span class="font-semibold">limited understanding</span> of how developers across different domains and contexts approach security in practice.

</div>

<div class="pt-8 text-lg max-w-3xl mx-auto opacity-90">

Different settings

- research labs, startups, industrial systems 

involve <span class="font-semibold">different constraints, priorities, and risk practices.</span>

</div>
</div>

---
transition: slide-left
layout: default
layoutClass: gap-12
---

# What I’m doing

<div class="ubuntu-window text-xl leading-snug max-w-4xl mx-auto">
<div class="text-lg leading-7">

### Empirical work
- surveys
- semi-structured interviews
- across research, commercial, and industrial contexts

### Focus
- workflows and tools  
- architectural decisions  
- how security is actually handled in practice  

<div class="pt-6 opacity-90">
Understanding how security is shaped by real-world constraints and decisions
</div>

</div>
</div>

---
transition: slide-left
layout: default
---

# Why this approach

<div class="ubuntu-window max-w-4xl mx-auto">

<div class="text-2xl leading-snug">
Secure systems emerge from the interaction between
</div>

<div class="pt-3 text-3xl leading-snug font-semibold">
architecture, tools, constraints, and developer judgement
</div>

<div class="pt-4 text-lg italic opacity-90">
not just technical controls in isolation
</div>

<div class="pt-8 text-xl">
If we ignore practice, we risk:
</div>

<ul class="pt-3 text-xl leading-relaxed">
  <li>barriers to adoption</li>
  <li>misalignment with real workflows</li>
</ul>

</div>
---
transition: slide-left
layout: default
---

# Closing

<div class="ubuntu-window max-w-4xl mx-auto">

<div class="text-2xl leading-snug">
If we want to improve security in robotics,
</div>

<div class="pt-3 text-xl opacity-90">
we need to understand not only the technology
</div>

<div class="pt-4 text-3xl font-semibold leading-snug">
but the practices through which systems are built
</div>

<div class="pt-10 text-lg opacity-85">
Early-stage work, feedback and conversations very welcome
</div>

</div>

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
