---
name: cmmc-credential
description: >
  Tracks and verifies CMMC competency credentials toward the Agent Skills Passport.
  Maps practice mastery, quiz scores, and simulation performance to credentialing
  milestones. Use when the user asks about their credentials, certification progress,
  portfolio, transcript, competency verification, Agent Skills Passport, or when
  the journey orchestrator reaches a credentialing checkpoint. Also triggers on
  "how am I doing overall," "am I ready for certification," "show my progress,"
  or "what have I earned."
---

# CMMC Credential Verification Skill

## Purpose
Transform learning activity data into structured competency credentials that feed
the Agent Skills Passport system.

## Credential Architecture

### Competency Levels (per practice)
| Level | Requirements |
|-------|-------------|
| Awareness | Studied at pattern/framework level |
| Understanding | Passed quiz at beginner level |
| Application | Passed quiz at intermediate level + completed 1 simulation |
| Proficiency | Scored accurately in simulation (within 1 point of ground truth) |
| Mastery | Proficient + can explain at system_of_systems level |

### Domain Credentials
| Credential | Requirements |
|-----------|-------------|
| Domain Aware | >50% practices at Awareness level |
| Domain Competent | >70% practices at Application level |
| Domain Proficient | >80% practices at Proficiency level |
| Domain Master | >90% practices at Mastery level |

### Assessment Credentials
| Credential | Requirements |
|-----------|-------------|
| Assessment Fundamentals | Completed 5+ single-practice simulations |
| Assessment Practitioner | Completed 3+ domain-wide simulations with >70% accuracy |
| Assessment Ready | All Critical domains at Domain Competent + full mock assessment |

## How to Generate a Credential Report

1. Call `session_progress` for overall stats
2. Call `coach_gap_analysis` for domain-level detail
3. Map the data to the credential architecture above
4. Present as a structured progress report:

```
╔══════════════════════════════════════════╗
║     CMMC L2 Competency Transcript       ║
║     Learner: [name if known]            ║
║     Date: [current date]                ║
╠══════════════════════════════════════════╣
║                                          ║
║  DOMAIN CREDENTIALS                      ║
║  ────────────────                        ║
║  AC  Access Control      ■■■■□  68%     ║
║      → Domain Competent (in progress)    ║
║  IA  Identification      ■■■□□  55%     ║
║      → Domain Aware (earned)             ║
║  SC  System & Comms      ■■□□□  38%     ║
║      → Working toward Domain Aware       ║
║                                          ║
║  ASSESSMENT CREDENTIALS                  ║
║  ──────────────────────                  ║
║  ✓ Assessment Fundamentals (8 sims)      ║
║  ◇ Assessment Practitioner (1/3 domain)  ║
║                                          ║
║  NEXT MILESTONES                         ║
║  ──────────────                          ║
║  → 2 more AC practices for Domain       ║
║    Competent                              ║
║  → Complete SC domain study to unlock    ║
║    Assessment Practitioner                ║
╚══════════════════════════════════════════╝
```

## Helm Program Course Mapping

Map credentials to the 6-course curriculum:

| Credential Area | Primary Course |
|----------------|---------------|
| Practice Knowledge | Context Engineering |
| Quiz Performance | Eval-driven Development |
| Simulation Skills | Workflow Orchestration |
| Evidence Analysis | Knowledge Reasoning |
| Assessment Technique | Prompt Engineering |
| Integration & Mastery | Agent-driven Coding |

## Artifact Generation

For consulting clients, offer to generate:
- PDF competency transcript (invoke pdf skill)
- Evidence portfolio checklist (invoke docx skill)
- Gap analysis report with remediation timeline (invoke docx skill)
- Assessment readiness scorecard (invoke xlsx skill)
