---
name: cmmc-scaffold-gap
description: >
  Bridges CMMC compliance mastery to The Scaffold's workforce diagnostic (PJRC framework)
  and identifies development gaps that extend beyond technical compliance into workforce
  capability. Use when the journey reaches a domain completion checkpoint, when the user
  asks about workforce readiness vs. technical compliance, when connecting CMMC learning
  to career development, or when generating Scaffold diagnostic updates. Also triggers on
  "workforce gap," "PJRC," "Scaffold diagnostic," "career development," "beyond compliance,"
  "what else do I need," or "how does this connect to my development."
---

# CMMC-to-Scaffold Gap Closure Skill

## Purpose
CMMC technical mastery is necessary but not sufficient. This skill maps compliance
learning to the broader PJRC workforce dimensions and identifies development gaps
that The Scaffold diagnostic would surface.

## The PJRC-CMMC Bridge

The Scaffold's PJRC framework measures four dimensions:
- **P**roduct Management — Can you scope, prioritize, and manage compliance programs?
- **J**udgment — Can you make defensible decisions in ambiguous assessment scenarios?
- **R**easoning — Can you connect technical controls to business risk and regulatory context?
- **C**ommunication — Can you explain compliance posture to executives, auditors, and teams?

### Mapping CMMC Activity to PJRC Dimensions

| CMMC Activity | Primary PJRC Dimension | Signal |
|--------------|----------------------|--------|
| Practice study (what/why faces) | Reasoning | Conceptual understanding |
| Practice study (how/apply faces) | Judgment | Implementation judgment |
| Quiz performance | Reasoning | Knowledge application |
| Simulation — interview quality | Communication | Assessment communication |
| Simulation — evidence requests | Product Management | Systematic assessment planning |
| Simulation — scoring accuracy | Judgment | Assessment judgment |
| Cross-practice navigation | Reasoning | Systems thinking |
| Gap analysis interpretation | Product Management | Strategic prioritization |

### Generating a PJRC Gap Analysis

After collecting sufficient CMMC activity data:

1. Call `session_progress` for activity breakdown
2. Call `coach_gap_analysis` for domain-level detail
3. Analyze PATTERNS in the data:

**Strong Reasoning, Weak Communication:**
"You understand the technical controls deeply (quiz scores averaging 85%)
but your simulation interviews tend to miss follow-up opportunities when
personnel give vague answers. This suggests a communication gap — you know
what to look for but struggle to elicit it from interviewees."

**Strong Judgment, Weak Product Management:**
"Your scoring accuracy is excellent (within 1 point of ground truth 80%
of the time) but you tend to assess practices in isolation rather than
following a systematic evidence collection plan. This suggests a product
management gap — you can evaluate well but need structure in your process."

### Recommending Development Actions

Based on PJRC gaps, recommend specific actions:

| PJRC Gap | Recommendation |
|----------|---------------|
| Product Management | Run domain-wide simulations to practice systematic assessment planning. Study the "when" and "where" cubelet faces for workflow integration. |
| Judgment | Increase simulation difficulty. Focus on edge-case scenarios. Study "apply" face failure modes. |
| Reasoning | Study cross-practice graph relationships. Use cmmc_practice_search for conceptual questions. Practice explaining "why" to non-technical stakeholders. |
| Communication | Re-run simulations focusing on interview technique. Practice crafting opening questions. Study the persona_relevance sections of "why" faces. |

### Helm Program Course Recommendations

Map PJRC gaps to specific courses:

| PJRC Dimension | Primary Helm Course | Rationale |
|---------------|-------------------|-----------|
| Product Management | Workflow Orchestration | Systematic process design |
| Judgment | Eval-driven Development | Evaluation frameworks and criteria |
| Reasoning | Context Engineering | Knowledge architecture and connections |
| Communication | Prompt Engineering | Structured communication with AI and humans |

## The Mirror Moment

At significant checkpoints (domain completion, assessment readiness), present
a "Mirror Moment" — The Scaffold's signature diagnostic reflection:

"You've reached a milestone. Let's take a moment to look at the full picture —
not just what you know about CMMC, but how you work with that knowledge.

Your technical mastery across Access Control is at 72%. That's strong.
But the way you got there tells a deeper story:

- Your quiz scores are consistently high (Reasoning: strong)
- Your simulation interviews often miss the third follow-up question
  (Communication: developing)
- You tend to score practices before requesting all available evidence
  (Product Management: developing)
- When you do score, you're remarkably accurate
  (Judgment: strong)

The Scaffold sees someone who KNOWS compliance deeply but needs to develop
the process discipline and interpersonal skills to PRACTICE it at a
professional level. That's exactly what the Workflow Orchestration and
Prompt Engineering courses are designed to address."

## Integration Points

- Feeds into The Scaffold's Work Reclassification diagnostic
- Updates Agent Skills Passport with PJRC dimension scores
- Informs Helm Program course sequencing recommendations
- Generates content for the learner's Scaffold newsletter profile
