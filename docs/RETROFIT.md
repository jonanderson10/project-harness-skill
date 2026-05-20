# Retrofit Mode — Apply Harness to Existing Codebase

**When:** You have an existing project (weeks/months/years old) with no harness docs.

---

## Phase 0: Scan the Codebase

The skill **automatically** scans your repo. No action needed from you.

**What the skill reads:**
- Folder structure (src/, lib/, components/, etc.)
- package.json / requirements.txt / go.mod (dependencies, scripts, entry points)
- Configuration files (astro.config.mjs, next.config.js, tsconfig.json, etc.)
- Existing docs (README.md, wiki/, docs/, comments in code)
- Key files (database schemas, API definitions, configuration)
- Git history (`git log --oneline -50`) — commit messages often surface decisions, pivots, and architectural shifts that no doc captures

**What the skill looks for:**
- Tech stack (framework, runtime, database, key dependencies)
- Architecture patterns (monolith, microservices, layered, domain-driven, etc.)
- Code organization (by feature, by type, by domain, etc.)
- Existing documentation (what's there, what's missing)
- Code comments that reveal intent or decisions

**Outcome of Phase 0:** Skill has a solid understanding of the codebase without asking you anything yet.

---

## Choosing a Mode

**Before asking any questions**, the skill presents this choice:

```
I've scanned your codebase. Before we start, which mode would you like?

  [S] Short  — 5 questions, ~5 min. Good-enough harness right away.
              Best when you want Claude working on your code today.

  [F] Full   — 9 phases, ~20–30 min. Deep harness with thorough rationale,
              design context, and decision log. Best for long-lived projects.

You can always deepen a Short harness later using Maintain mode.

Type S or F to continue.
```

---

## Short Mode

The skill asks **5 focused questions** covering 80% of the value:

1. **What is this?** — "I see [tech/patterns]. What's the purpose and who uses it?"
2. **Why this stack?** — "You're using [framework + db]. Why those choices over alternatives?"
3. **What were the biggest decisions?** — "What 2–3 architectural choices most shaped this codebase?"
4. **Walk me through the folder structure** — "What goes where, and why is it organized that way?"
5. **Any gotchas?** — "What would surprise a developer reading this code for the first time?"

The skill generates the full harness immediately after. Trade-off: DESIGN.md and DECISIONS.md will be thinner — deepen them over time with Maintain mode.

---

## Full Mode: Phase 1 — Understand Product & Purpose

**Goal:** Confirm what this project is and who uses it — the code rarely tells the full story.

Ask: what is it and who uses it; what's explicitly out of scope; what stage is it in (early/stable/maintenance). Show what you inferred from the code and ask for corrections.

**Outcome:** Clear understanding of purpose, users, scope, and project stage.

---

## Phase 2: Extract Technical Architecture

**Goal:** Understand *why* the tech choices were made, not just what they are.

Ask: why this stack over alternatives; walk me through the data model and constraints; any integrations, performance requirements, or testing strategy worth documenting.

**Outcome:** Technical decisions captured with rationale, not just inventory.

---

## Phase 3: Identify Key Decisions & Constraints

**Goal:** Surface the 2–3 decisions that most shaped the architecture.

Ask: what are the biggest architectural decisions; any non-negotiable constraints (compliance, platform, performance); what trade-offs were made consciously.

**Outcome:** The "why behind the why" — decisions that would confuse anyone reading the code cold.

---

## Phase 4: Understand the User Experience & Design

**Goal:** Document the user-facing side. Skip or abbreviate for backend/library projects.

Ask: walk me through the primary user journey; any design guidelines or component library; tone, style, and accessibility requirements.

**Outcome:** Enough context to generate DESIGN.md or know it's not applicable.

---

## Phase 5: Map the Codebase

**Goal:** Understand the directory structure and how developers navigate it.

Ask: walk me through the directory structure — what lives where and why; how are new features built; where do new developers struggle most.

**Outcome:** Folder structure and conventions documented; non-obvious coupling flagged.

---

## Phase 6: Identify Missing Context

**Goal:** Catch anything the code doesn't reveal.

Ask: any gotchas or surprises; deployment process and security considerations; anything else you want documented that hasn't come up.

**Outcome:** Skill has complete context. No important knowledge left undocumented.

---

## Phase 7: Generate the Harness

The skill **automatically generates** all the docs based on everything you've told it:

**Generates:**
- **CLAUDE.md** — Entry point for agents; maps to other docs
- **README.md** — For humans discovering the project
- **docs/PRODUCT_SENSE.md** — What, who, why, scope
- **docs/DESIGN.md** (or **docs/ARCHITECTURE.md**) — Visual direction and/or system architecture
- **docs/TECHNICAL.md** — Stack, setup, folder structure, how things work
- **docs/DECISIONS.md** — Major decisions with rationale and trade-offs
- **docs/references/** (optional) — Data model, architecture patterns, etc.
- **.claude/commands/** — audit.md, decision.md, sync-docs.md

**What it includes:**
- All the context you provided
- Inferred architecture and patterns
- Code organization explained
- Decision log with your rationale
- Setup instructions extracted from code

**What you do:**
- Review the generated docs
- Correct anything the skill got wrong
- Add nuance or additional detail
- Adjust tone or emphasis

---

## Phase 8: Review & Refine

You review what the skill generated. For each doc:

**Check:**
- Is this accurate? (Does it match the code and your intent?)
- Is anything missing? (Important context, constraints, patterns?)
- Is it clear? (Would a new developer understand this?)
- Does it match the tone and style you want?

**Edit:**
- Fix inaccuracies
- Add missing context
- Clarify confusing sections
- Adjust examples or formatting

**Commit:**
- Once you're satisfied, commit the harness alongside your code
- Claude Code now reads CLAUDE.md at session start and understands the entire project

**Outcome of Phase 8:** Your project now has a complete harness. Any agent reads CLAUDE.md at session start and understands what you've built, why you built it that way, and how to work with it.

---

## Example Full Workflow

See [docs/RETROFIT_WORKFLOW.md](docs/RETROFIT_WORKFLOW.md) for a complete walkthrough of a full Retrofit session.

---

## Interview Tips for Retrofit

**For the skill (when interviewing you):**

- **Ask concrete questions** — "Why did you choose X?" not "Tell me about your architecture"
- **Show what you see** — "I notice you're using [pattern]. Help me understand why"
- **Follow up** — "You said [X]. Can you give me an example?"
- **Clarify trade-offs** — "What did you give up by choosing this?"
- **Don't assume** — Ask, don't guess

**For you (when answering):**

- **Be specific** — "We use GraphQL because REST didn't fit our use case" not "GraphQL is better"
- **Explain context** — "We were originally on REST, but switched when..."
- **Share constraints** — "We had to do this because..."
- **Flag gotchas** — "This part is messy because..."
- **Correct the skill** — "Actually, that's not quite right. Here's what's really happening..."

---

## Monorepo Note

If your project is a monorepo (multiple packages, workspaces, Turborepo, nx, etc.):

- Place a root `CLAUDE.md` that references per-package CLAUDE.md files
- Each package gets its own harness doc set
- The root CLAUDE.md maps to the full structure

Example root CLAUDE.md:
```
# MyMonorepo

## Packages
- [apps/web](apps/web/CLAUDE.md)
- [apps/api](apps/api/CLAUDE.md)
- [packages/ui](packages/ui/CLAUDE.md)
```