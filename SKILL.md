---
name: project-harness
description: Create and maintain agent-ready project infrastructure. Use this skill to SETUP (scaffold new project), RETROFIT (reverse-engineer from existing code), MAINTAIN (keep docs current), or AUDIT (verify freshness). The skill detects your situation automatically. Works for any project type.
---

# Claude Project Harness

One skill for the full harness lifecycle: **create, retrofit, maintain, audit.**

The core principle: `CLAUDE.md` is the automatic entry point for agents — it's loaded at session start. Everything agents need lives in the repository. This skill ensures that content is created, stays current, and stays accurate.

---

## Detection Flow

When you invoke this skill, it detects your situation:

```
↓ Does CLAUDE.md exist?

YES → Read it, then:
      ├─→ Update/maintain the code? → MAINTAIN MODE
      ├─→ Check if docs are current? → AUDIT MODE
      └─→ Start over from scratch? → SETUP MODE

NO → Is there existing code?
     ├─→ YES → RETROFIT MODE (reverse-engineer from code)
     └─→ NO → SETUP MODE (create from scratch)
```

**If CLAUDE.md exists but is empty or stale**, treat it as a Retrofit situation.

---

## Four Modes

| Mode | When to Use | Docs |
|------|-------------|------|
| **Setup** | Starting a brand new project | [docs/SETUP.md](docs/SETUP.md) |
| **Retrofit** | Existing code, no harness docs | [docs/RETROFIT.md](docs/RETROFIT.md) |
| **Maintain** | Active development, keep docs in sync | [docs/MAINTAIN.md](docs/MAINTAIN.md) |
| **Audit** | Periodic health check | [docs/AUDIT.md](docs/AUDIT.md) |

---

## Core Principles (All Modes)

1. **Agent-legible first** — Docs structured so any agent understands scope from repo alone
2. **Progressive disclosure** — CLAUDE.md (~100 lines) → detailed docs via relative links
3. **Living documentation** — Docs reflect reality; update them as code changes
4. **No hidden context** — Everything lives in the repo
5. **Decisions recorded** — Why you chose X goes in DECISIONS.md

---

## Standard Harness Structure

The harness is a **documentation overlay** — it adds files to the root and a `docs/` folder. It does not prescribe how your code is organized.

```
project-root/
├── CLAUDE.md              # Entry point for agents (~100 lines)
├── README.md              # Human overview
├── .claude/
│   └── commands/
│       ├── audit.md        # /audit — run harness health check
│       ├── decision.md    # /decision — log a new decision
│       └── sync-docs.md   # /sync-docs — update docs after changes
└── docs/
    ├── PRODUCT_SENSE.md   # What, who, why, scope
    ├── DESIGN.md          # Visual/UX direction (or ARCHITECTURE.md)
    ├── TECHNICAL.md       # Stack, setup, folder structure
    ├── DECISIONS.md       # Decision log with rationale
    └── references/        # (Optional) Tech guides, data models
```

Your source code lives wherever it already lives. TECHNICAL.md describes that structure.

---

## Templates

This skill includes templates for different project types. See [TEMPLATES.md](TEMPLATES.md) for:
- Website / Static Site
- Internal Tool / Dashboard
- API / Backend Service
- Generic Project

Each template includes starter versions of CLAUDE.md, PRODUCT_SENSE.md, DESIGN.md, TECHNICAL.md, and DECISIONS.md.

---

## Anti-Patterns to Avoid

- **The mega CLAUDE.md** — Keep it under 100 lines; use linked docs for detail
- **Hidden context in Slack** — Agents can't read threads
- **Outdated docs** — Code changes, docs don't; agents make wrong assumptions
- **No decision log** — "Why did we choose X?" has different answers in three places
- **No success criteria** — Agents don't know what "done" means

---

## CLAUDE.md Guidelines

**Use relative links** — `[PRODUCT_SENSE.md](docs/PRODUCT_SENSE.md)` — works across all models and tools.

**Keep total context under ~500 lines** — CLAUDE.md + all linked docs combined.

**Only link to current docs** — stale imports are worse than no imports.

---

## Next Steps

1. **Invoke the skill** with your situation
2. **Skill detects mode** and routes to the appropriate doc
3. **Work through the mode**
4. **Commit the harness** alongside your code
5. **Maintain over time** using Maintain and Audit modes

---

*Skill updated: 2026-05-19*
*Originally based on "Harness Engineering" (Ryan Lopopolo) — adapted for Claude Code*