# CMMC Cubelet Plugin

**AI-native CMMC compliance learning, simulation, credentialing, and gap closure — all in the flow of work.**

## What This Plugin Does

Instead of giving you 16 separate MCP tools and asking you to figure out the sequence, this plugin **orchestrates** the entire CMMC compliance learning journey:

```
Study → Quiz → Simulate → Verify Credentials → Close Diagnostic Gaps → Plan Next Steps
```

The orchestrator adapts to three personas:

| Persona | Experience | The Plugin Does |
|---------|-----------|----------------|
| **Helm Program Student** | Learning CMMC from scratch | Full pedagogical sequence with maturity progression |
| **Compliance Professional** | Knows CMMC, needs practice | Simulation-heavy, edge-case focused, gap closure |
| **Consulting Client** | Preparing an org for assessment | Guided readiness with exportable deliverables |

## Installation

```bash
# From GitHub marketplace
/plugin marketplace add cmmc-cubelet/cmmc-cubelet-plugin
/plugin install cmmc-cubelet@9brains-cmmc-cubelet-plugin

# Or local development
claude --plugin-dir ./cmmc-cubelet-plugin
```

## Commands

| Command | What It Does |
|---------|-------------|
| `/cmmc-cubelet:start-journey` | Begin or resume your adaptive learning journey |
| `/cmmc-cubelet:simulate` | Run an assessment simulation (optionally specify practice/domain) |
| `/cmmc-cubelet:my-progress` | View credentials, mastery levels, and next milestones |
| `/cmmc-cubelet:generate-report` | Create consulting deliverables (gap reports, POA&Ms, scorecards) |

## Skills (Auto-Invoked)

These activate contextually — you don't need to call them directly:

| Skill | Triggers When |
|-------|--------------|
| `cmmc-journey` | Any CMMC learning request — the main orchestrator |
| `cmmc-study` | Studying a specific practice or concept |
| `cmmc-simulate` | Running assessment simulations |
| `cmmc-credential` | Checking progress or credential status |
| `cmmc-scaffold-gap` | Connecting compliance to workforce development |

## Agents

| Agent | Role |
|-------|------|
| `assessment-coach` | Real-time coaching during simulations |
| `gap-analyst` | Generates consulting deliverables |

## MCP Integration

Connects to the **CMMC Cubelet Platform** (`cmmc.cubelet.ai/mcp`) which provides:
- 110 CMMC Level 2 practices with 6-face, 5-maturity-level knowledge architecture
- Adaptive coaching engine with gap analysis
- Procedurally generated assessment simulations with ground-truth scoring
- Persistent learner progress tracking
- Semantic search across practices, quizzes, and documentation

## Architecture

```
┌─────────────────────────────────────────────────┐
│              CMMC Cubelet Plugin                 │
│                                                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────────┐  │
│  │  Skills   │  │  Agents  │  │   Commands   │  │
│  │           │  │          │  │              │  │
│  │ journey   │  │ assess-  │  │ start-       │  │
│  │ study     │  │ coach    │  │ journey      │  │
│  │ simulate  │  │          │  │ simulate     │  │
│  │ credential│  │ gap-     │  │ my-progress  │  │
│  │ scaffold  │  │ analyst  │  │ generate-    │  │
│  │ -gap      │  │          │  │ report       │  │
│  └─────┬─────┘  └────┬─────┘  └──────┬───────┘  │
│        │             │               │           │
│  ┌─────┴─────────────┴───────────────┴─────┐    │
│  │           Journey Orchestrator           │    │
│  │  (cmmc-journey SKILL.md = program.md)    │    │
│  └─────────────────┬───────────────────────┘    │
│                    │                             │
│  ┌─────────────────┴───────────────────────┐    │
│  │         Hooks (SessionStart, Stop)       │    │
│  └─────────────────┬───────────────────────┘    │
└────────────────────┼─────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────┐
│         CMMC Cubelet Platform (MCP)              │
│                                                  │
│  practice_list    coach_explain     simulation_  │
│  practice_get     coach_feedback    start        │
│  practice_search  coach_gap_        simulation_  │
│  domain_get       analysis          interview    │
│  quiz_get         coach_recommend_  simulation_  │
│                   next              score        │
│                   session_progress  simulation_  │
│                                     status       │
└─────────────────────────────────────────────────┘
```

## The Karpathy Parallel

This plugin applies the `program.md` pattern from [autoresearch](https://github.com/karpathy/autoresearch):

| autoresearch | CMMC Cubelet Plugin |
|-------------|-------------------|
| `program.md` — instructions, constraints, stopping criteria | `cmmc-journey/SKILL.md` — persona logic, thresholds, anti-patterns |
| `train.py` — the editable artifact | Learner mastery state — evolves with each interaction |
| `val_bpb` — the scalar metric | Domain mastery % and simulation scoring accuracy |
| 5-min time-boxed cycle | Study → Quiz → Simulate → Verify loop |
| Git as memory | session_progress as persistent state |

The human doesn't orchestrate. The system does. The human just engages.

## The Scaffold Integration

At natural checkpoints, the plugin bridges to The Scaffold's PJRC diagnostic:
- Maps CMMC activity to Product Management, Judgment, Reasoning, Communication
- Identifies workforce capability gaps beyond technical compliance
- Recommends Helm Program courses for development
- Delivers the "Mirror Moment" — a reflective diagnostic that shows not just
  what you know, but how you work with what you know

## License

Proprietary — 9BRAINS / Divergence Academy / Euler Center
