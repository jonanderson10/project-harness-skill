# Setup Mode — Create Harness for New Project

**When:** You're starting a brand new project with no code yet.

---

## Phase 1: Capture Project Scope

The skill asks about your project:

1. **What is this?** — "Describe the project in 2–3 sentences. What does it do?"
2. **Who uses it?** — "Who is the primary user? Are there secondary users?"
3. **Core features** — "What are the main features, pages, or functionality?"
4. **Out of scope** — "What are you explicitly NOT building?"
5. **Stage** — "Early development, beta, stable?"

Show what you inferred and ask for corrections.

**Outcome:** Clear understanding of purpose, users, scope, and project stage.

---

## Phase 2: Set Up Repository Structure

Ask how the user plans to organize their code (or if they already have a structure in mind).

Create the harness doc layer:
- Root files: `CLAUDE.md`, `README.md`
- `docs/` directory
- `.claude/commands/` directory

**Important:** The harness does not prescribe source code structure. That structure is described in TECHNICAL.md. The harness drops in alongside existing code.

### What to Create

```
project-root/
├── CLAUDE.md              # Entry point for agents
├── README.md              # Human overview
├── .claude/
│   └── commands/
│       ├── audit.md       # /audit — run harness health check
│       ├── decision.md    # /decision — log a new decision
│       └── sync-docs.md   # /sync-docs — update docs after changes
└── docs/
    └── references/       # (Optional) Tech guides, data models
```

The `.claude/commands/` files are provided by TEMPLATES.md. Copy them from the generic template.

---

## Phase 3: Write CLAUDE.md

Use TEMPLATES.md as a starting point. The template gives you the structure; customize it with your project info.

**CLAUDE.md structure:**
- Quick Facts: project name, status, stack, primary purpose
- Key Principles: 2–3 guiding values
- Documentation: links to other docs
- Custom Commands: note the slash commands

**Rules:**
- Keep CLAUDE.md to ~50–100 lines of orientation
- Use relative links for docs (e.g., `[PRODUCT_SENSE.md](docs/PRODUCT_SENSE.md)`) — works across all models
- Only link to docs that are current; stale links are worse than no links

---

## Phase 4: Write Core Reference Docs

For each doc, use TEMPLATES.md as a starting point:

### docs/PRODUCT_SENSE.md

- What is this? (2–3 sentences)
- Who is it for? (primary + secondary users)
- Core features / pages / functionality
- What's NOT in scope (explicit exclusions)
- Success criteria
- Key constraints

### docs/DESIGN.md (or docs/ARCHITECTURE.md)

**Use DESIGN.md** for user-facing projects (websites, apps, dashboards).
**Use ARCHITECTURE.md** for code-focused projects (APIs, libraries, backend services).

- Visual direction or system overview
- Color palette / typography (DESIGN) or tech stack (ARCHITECTURE)
- Layout patterns or component interactions
- Component library if applicable

### docs/TECHNICAL.md

- Stack (runtime, framework, database, key deps)
- Why these choices?
- Setup & local development (prerequisites, install, run)
- Project structure (describe actual structure, don't prescribe)
- Common tasks (how to update config, add a page, deploy)
- Build & deployment

---

## Phase 5: Create docs/DECISIONS.md

Log any decisions already made:
- What was chosen and why
- Alternatives considered
- Trade-offs made

If no decisions are ready yet, create the file with a header and note "Add decisions as they come up."

---

## Phase 6: Set Up docs/references/ (Optional)

If there are important references (data models, architecture patterns, tech guides), create them here.

This is optional — only create references that are complex enough to warrant their own doc.

---

## Phase 7: Write README.md

For humans discovering the project:
- One-line description
- What it does / who it's for
- Quick start (clone, install, run)
- Key links to docs

---

## Example Workflow

```
You: "Create a harness for my new web app"

Skill: [asks Phase 1 questions]
       "What is this? Who uses it? Core features? Technical decisions?"

You: [answers - "It's a project management tool for small teams.
       PMs and team leads use it. Features: task boards, due dates,
       comments. Not building time tracking or invoicing. Early stage."]

Skill: [Phase 2]
       "How are you organizing your code? Do you have a structure in mind?"

You: "I'll use Next.js with app router, src/ folder for code."

Skill: [Phase 3-7 - generates CLAUDE.md, README.md, docs/PRODUCT_SENSE.md,
        docs/DESIGN.md, docs/TECHNICAL.md, docs/DECISIONS.md, .claude/commands/]

You: [reviews]
     "Perfect, commit it"
```

**Outcome:** Brand new project with clear structure. Ready for agents to work on.

---

## Interview Tips for Setup

**For the skill (when interviewing):**
- Ask concrete questions — "What's the primary user task?" not "Tell me about UX"
- Show what you inferred — "I see you're using Next.js. App router or pages?"
- Follow up — "You said [X]. Can you give me an example?"
- Don't assume — Ask, don't guess

**For you (when answering):**
- Be specific — "Next.js with app router" not "React"
- Explain context — "We chose this because..."
- Flag gotchas — "We're still figuring out auth"
- Correct the skill — "Actually, that's not quite right"