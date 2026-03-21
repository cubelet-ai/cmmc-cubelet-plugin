---
name: cmmc-study
description: >
  Deep-dive study of individual CMMC practices using the Cubelet six-face model
  (What/Why/How/Where/When/Apply) across five maturity levels. Use this skill when
  the user asks to study, learn about, understand, or explore a specific CMMC practice,
  domain, or concept — or when the journey orchestrator delegates a teaching moment.
  Also triggers on questions like "explain access control," "what is CUI encryption,"
  "how does MFA work for CMMC," or any CMMC practice reference by ID (e.g., AC.L2-3.1.1).
---

# CMMC Practice Study Skill

## Purpose
Teach a single CMMC practice deeply using the Cubelet's multi-face, multi-maturity
knowledge architecture. This skill is called by the journey orchestrator OR directly
by a user who wants to explore a specific practice.

## Teaching Sequence

### 1. Identify the Practice
If the user gives a practice ID (e.g., "AC.L2-3.1.1"), use it directly.
If they describe a concept, use `cmmc_practice_search` to find the matching practice(s).
If multiple matches, present the top 3 and let them choose.

### 2. Assess Entry Level
Check `session_progress` for existing mastery on this practice.
- Unknown/Novice → start at PATTERN maturity level
- Developing → start at FRAMEWORK level
- Proficient → start at SYSTEM level
- Expert → start at SYSTEM_OF_SYSTEMS or COGNITIVE_CORE level

### 3. Teach Using Faces

Call `coach_explain` with the practice_id and appropriate face.

Teaching sequence varies by context:
- **First encounter**: what → why → how (build conceptual foundation)
- **Pre-simulation prep**: how → apply → when (build practical readiness)
- **Gap remediation**: why → where → apply (reconnect to purpose)

When presenting face content:
- TRANSLATE the cubelet data into natural teaching. Don't read JSON aloud.
- USE the analogy from the "how" face to anchor understanding.
- CONNECT to the user's context — if they mentioned their organization, reference it.
- HIGHLIGHT graph relationships: "This practice REQUIRES IA.L2-3.5.1, which means
  you can't fully implement access control without identification. They're linked."

### 4. Evidence Awareness

Call `cmmc_practice_get` to retrieve the evidence_checklist and scoring_criteria.

For students: present evidence as "what an assessor would look for"
For professionals: present as a self-assessment checklist
For clients: present as "what you need to have ready"

### 5. Comprehension Check

Ask ONE scenario-based question that requires applying the practice, not
just recalling definitions. Example:

"You're reviewing a 50-person defense contractor. They use Active Directory
but you discover three shared accounts for the CNC machines on the shop floor.
How would you assess AC.L2-3.1.1 for this finding?"

### 6. Cross-Practice Navigation

After teaching, surface graph_relationships from the cubelet data:
- "This practice REQUIRES [X] — want to study that dependency first?"
- "This practice ENABLES [Y] — that's a natural next step."
- "This practice is CONSTRAINED BY [Z] — worth understanding the boundary."

## Maturity Level Guidance

| Level | Audience | Depth |
|-------|----------|-------|
| Pattern | Beginners, first exposure | Analogies, simple definitions |
| Framework | Students with some context | Structured explanations, boundaries |
| System | Practitioners | Technical implementation, variables |
| System of Systems | Experienced professionals | Cross-system integration |
| Cognitive Core | Expert assessors | Judgment, edge cases, nuance |

## Search Integration

If the user asks a question that spans multiple practices (e.g., "how should I
handle shared service accounts?"), use `cmmc_practice_search` with their natural
language query. Present the top results with relevance context, then offer to
deep-dive into the most relevant practice.
