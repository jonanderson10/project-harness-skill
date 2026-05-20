# Project Harness Skill

A unified, general-purpose skill for creating and maintaining agent-ready project infrastructure.

**Works for any situation:** new projects, existing codebases, active development, and verification.

## Core Principles

1. **Agent-legible first** — Docs structured so AI understands scope from repo alone
2. **Progressive disclosure** — CLAUDE.md (~100 lines) → detailed references
3. **Living documentation** — Docs updated as code changes
4. **No hidden context** — Everything lives in the repo
5. **Decisions recorded** — Why you chose X should be in DECISIONS.md

## What You Get

By using this skill, you enable:

- **Faster agent comprehension** — Agents understand scope without constant clarification
- **Better consistency** — Decisions are documented, patterns are explicit
- **Easier handoff** — New team members (human or AI) get up to speed faster
- **Less technical debt** — Decisions and trade-offs are recorded, not forgotten
- **Fresh documentation** — Docs stay in sync with code

## One Skill, All Situations

| Situation | Mode | You Need |
|-----------|------|----------|
| Starting a new project | Setup | Create harness scaffolding |
| Existing code, no docs | Retrofit | Reverse-engineer harness from code |
| Actively developing | Maintain | Keep docs in sync with code |
| Periodic check | Audit | Verify docs are current |

### Using the Skill Over Time

**Day 1:** Setup mode → Create harness from scratch
**Days 2–30:** Maintain mode → Build code, update docs
**Day 30:** Audit mode → Spot check for drift
**Day 60:** Maintain mode → Continue, keep docs fresh

The skill grows with your project.

## Next Steps

1. **Install the skill** in your LLM interface
2. **Invoke it** with your situation (new/existing/active/check)
3. **Skill detects** and recommends mode
4. **Follow the guidance** for that mode
5. **Commit** the harness alongside your code
6. **Maintain over time** using Maintain and Audit modes


---

**Inspired by:** "Harness Engineering: Leveraging Codex in an Agent-First World" (Ryan Lopopolo, 2026)

## Installation

### Claude Code

```bash
cp -r .claude/skills/project-harness ~/.claude/skills/
```

### OpenCode

```bash
mkdir -p ~/.opencode/skills && cp -r .claude/skills/project-harness ~/.opencode/skills/
```

### Cursor

```bash
cp -r .claude/skills/project-harness your-project/.cursor/skills/
```

> **Note:** Cursor requires Nightly channel and Agent Skills enabled in Settings.

### Codex CLI

```bash
mkdir -p ~/.agents/skills && cp -r .claude/skills/project-harness ~/.agents/skills/
```

Restart your session. The skill activates automatically when invoked.

## What's Inside

- **SKILL.md** — Core skill with detection logic and mode summaries
- **docs/** — Detailed mode workflows (SETUP.md, RETROFIT.md, MAINTAIN.md, AUDIT.md)
- **TEMPLATES.md** — Ready-to-use templates for different project types

## Key Features

### Four Modes (Skill Detects Which You Need)

1. **Setup** — Create harness from scratch for new projects
2. **Retrofit** — Reverse-engineer harness from existing code
3. **Maintain** — Keep harness current as code evolves
4. **Audit** — Verify docs are fresh and complete

### Smart Detection

The skill automatically figures out your situation:

```
You invoke the skill

↓ Skill checks: Does CLAUDE.md exist?

YES → You already have a harness
      ├─→ Want to maintain/update? → MAINTAIN MODE
      ├─→ Want to verify it's current? → AUDIT MODE
      └─→ Start over? → SETUP MODE

NO → Skill asks: Is there existing code?
     ├─→ YES → RETROFIT MODE (reverse-engineer from code)
     └─→ NO → SETUP MODE (create from scratch)
```

## How to Use

### Workflow

**New Project:**
```
You: "Create a harness for my new web app"

Skill: [detects no CLAUDE.md, no code]
       → SETUP MODE
       → Guides you through 7 phases
       → Generates CLAUDE.md, PRODUCT_SENSE.md, DESIGN.md, TECHNICAL.md, etc.
```

**Existing Code:**
```
You: "Create a harness for this project"

Skill: [detects no CLAUDE.md, sees code]
       → RETROFIT MODE
       → Scans codebase, asks questions
       → Generates harness from code + your answers
```

**Active Development:**
```
You: "I refactored the auth system. Update the docs?"

Skill: [detects CLAUDE.md exists]
       → MAINTAIN MODE
       → Updates TECHNICAL.md, logs decisions, detects drift
```

**Health Check:**
```
You: "Audit the harness. What's stale or missing?"

Skill: [detects CLAUDE.md exists]
       → AUDIT MODE
       → Compares code vs. docs
       → Reports findings with recommendations
```

## The Entry Point: CLAUDE.md

Every harness has **CLAUDE.md** at the root. It's the entry point — agents read it at the start of every session to understand the project:

1. Agent clones repo
2. Agent reads CLAUDE.md (~2 min)
3. Agent follows the map to understand the project
4. Agent uses this skill if they need to update/maintain the harness
5. Agent starts working

No magic. No hidden context. The repo documents itself.

## Harness Structure

Every harness follows the same structure:

```
project-root/
├── CLAUDE.md              # Entry point for agents
├── README.md              # Human overview
├── .claude/
│   └── commands/          # Custom slash commands
│       ├── audit.md
│       ├── decision.md
│       └── sync-docs.md
└── docs/
    ├── PRODUCT_SENSE.md   # What, who, why
    ├── DESIGN.md          # Visual/UX direction (or ARCHITECTURE.md)
    ├── TECHNICAL.md       # Stack, setup, folder structure
    ├── DECISIONS.md       # Why did you choose X?
    └── references/        # (Optional) Tech guides, patterns
```

Your source code lives wherever it already lives. TECHNICAL.md describes that structure — the harness doesn't change it.

## Templates

The skill includes templates for:
- **Websites / Static Sites** (TEMPLATES.md)
- **Dashboards / Internal Tools** (TEMPLATES.md)
- **APIs / Backend Services** (TEMPLATES.md)
- **Generic Projects** (TEMPLATES.md)

Use these as starting points and customize for your project.
