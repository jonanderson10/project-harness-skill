# Agent Harness Templates

One template set for all project types. Templates are in the `templates/` directory.

## What's in `templates/`

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Entry point for agents (~100 lines) |
| `PRODUCT_SENSE.md` | What, who, why, scope |
| `DESIGN.md` | Visual/UX direction (use ARCHITECTURE.md for code-focused) |
| `ARCHITECTURE.md` | System architecture (alternative to DESIGN.md) |
| `TECHNICAL.md` | Stack, setup, folder structure |
| `DECISIONS.md` | Decision log with rationale |
| `commands/audit.md` | `/audit` slash command |
| `commands/decision.md` | `/decision` slash command |
| `commands/sync-docs.md` | `/sync-docs` slash command |

---

## How to Use

1. Copy files from `templates/` to your project root
2. Replace `[BRACKETS]` with your actual info
3. Delete sections marked "OPTIONAL" if not applicable
4. Customize for your project type (see below)
5. Read `CLAUDE.md` to understand what to do next

---

## Project Type Customization

### Website / Static Site
- Use `DESIGN.md` as-is (focus on visual design)
- Focus `TECHNICAL.md` on: framework (Astro/Next/11ty?), build process, asset management, deployment

### Internal Tool / Dashboard
- Use `ARCHITECTURE.md` instead of `DESIGN.md` (focus on system structure)
- Focus `TECHNICAL.md` on: stack, setup, folder structure, how data flows
- Add detailed references in `docs/` for data model, API endpoints, etc.

### API / Backend Service
- Use `ARCHITECTURE.md` instead of `DESIGN.md`
- Focus `TECHNICAL.md` on: runtime, framework, database, how to run tests, how to deploy
- Add `docs/references/` with: endpoint documentation, data model, error handling strategy

### Generic Project
- Use templates as-is

---

## CLAUDE.md Guidelines

- Keep it under 100 lines
- Use relative links to detail docs: `[PRODUCT_SENSE.md](docs/PRODUCT_SENSE.md)`
- Only link to current docs — stale imports are worse than no imports
- Total loaded context (CLAUDE.md + all linked docs) should stay under ~500 lines

---

*Skill updated: 2026-05-19*