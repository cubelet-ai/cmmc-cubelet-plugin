---
name: cmmc-simulate
description: >
  Runs interactive CMMC assessment simulations where learners practice as either
  assessors (conducting interviews, requesting evidence, scoring practices) or
  auditees (responding to assessment questions, presenting evidence, defending posture).
  Use this skill when the user wants to practice an assessment, run a simulation,
  do a mock assessment, practice interviewing, prepare for a C3PAO visit, test their
  scoring ability, or when the journey orchestrator transitions to simulation phase.
  Also triggers on "let me practice," "mock audit," "assessment drill," or
  "simulate an assessment."
---

# CMMC Assessment Simulation Skill

## Purpose
Run realistic CMMC Level 2 assessment simulations against procedurally generated
companies. The simulation engine provides named personnel, realistic environments,
and ground-truth scoring for feedback.

## Simulation Flow

### 1. Configure the Simulation

Determine role based on persona:
- **Assessor role** (default for students & professionals): User conducts the assessment.
  They interview company personnel, request evidence, and score practices.
- **Auditee role** (for consulting clients): User is being assessed. They respond to
  questions and present their organization's posture.

Determine scope:
- Single practice (default, used during learning loops)
- Domain-wide (when domain mastery > 50%, cover all practices in a domain)
- Full assessment (when overall mastery > 50%, multi-domain simulation)

Call `simulation_start` with role and optional practice_ids.

### 2. Present the Company

The simulation returns a company profile with:
- Company name, industry, size, location
- DoD contract context and CUI types
- Key personnel with names, roles, and tags
- IT environment details
- Security maturity level

Present this as a briefing, not raw data:
"You've been assigned to assess Iron Hawk Defense Technologies, a 234-person
weapons systems manufacturer in Phoenix. They hold Army PEO Missiles & Space
contracts and handle Export Control, Proprietary, and CTI data types. Their
IT Director Christopher Lee will be your primary technical contact."

### 3. Guide the Assessment (Assessor Role)

**Interview Phase:**
- Suggest opening questions that target the practice under assessment
- After each response, analyze what was said and suggest follow-up angles
- Coach the user on effective interview technique:
  "Good question. Notice how the IT Director mentioned 'most systems' — that
  qualifier suggests there might be gaps. Follow up on which systems are excluded."

Use `simulation_interview` for each exchange. The simulation provides realistic
responses from the company's named personnel.

**Evidence Phase:**
- After 2-4 interview exchanges, prompt the user to request evidence
- Suggest specific evidence types based on what the interview revealed
- Use `simulation_request_evidence` to get the simulated evidence

"Based on what Christopher said about Active Directory, you should request
their GPO documentation and user provisioning procedures."

**Scoring Phase:**
- When enough information is gathered, prompt the user to score
- Remind them of the scoring criteria: Met (3), Largely Met (2), Not Met (0)
- Ask them to justify their score before submitting
- Use `simulation_score` to submit and get feedback against ground truth

"Before I submit your score, walk me through your reasoning. Why Largely Met
instead of Met? What specific gap justifies a 2 instead of a 3?"

### 4. Guide the Assessment (Auditee Role)

**Preparation:**
- Before the simulation asks questions, help the user prepare
- Surface the evidence checklist for the practice being assessed
- Discuss what a strong response looks like

**Response Coaching:**
- When the simulated assessor asks a question, help craft the response
- Flag when the user's response might raise red flags
- Suggest evidence to proactively offer

**Gap Identification:**
- After the exchange, help identify gaps in their posture
- Connect gaps to specific remediation actions

### 5. Debrief

After scoring:
1. Present the ground truth comparison
2. Analyze where the user's assessment diverged from expected
3. Identify patterns (too lenient? too strict? missing evidence types?)
4. Call `coach_feedback` for personalized guidance
5. Record the result via `session_progress`

## Simulation Coaching Tips

Weave these naturally into the simulation:

- "An experienced assessor would dig deeper here — the response was vague
  about how often access reviews happen."
- "Notice the Compliance Officer jumped in unprompted. That sometimes
  indicates the IT Director is uncomfortable with the question."
- "Three evidence items support a Met score here, but the lack of automated
  monitoring means Largely Met is more defensible."

## Session Management

- Track simulation state via `simulation_status`
- If the user needs to pause, note the session_id and current phase
- If the simulation completes, call `session_reset` to clean up
- Always call `session_progress` after simulation to update mastery
