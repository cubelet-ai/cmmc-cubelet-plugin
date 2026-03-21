---
description: Run a CMMC assessment simulation. Optionally specify a practice ID or domain to focus on, or let the coaching engine choose based on your readiness.
---

Launch a CMMC assessment simulation using the cmmc-simulate skill.

If I specified a practice (e.g., /simulate AC.L2-3.1.1) or domain (e.g., /simulate AC),
scope the simulation accordingly.

If I didn't specify, use coach_recommend_next to pick the highest-value practice
for simulation based on my current mastery state.

Set up the simulation, brief me on the company, and begin. Use the assessment-coach
agent to provide real-time guidance during the simulation.

Arguments: $ARGUMENTS
