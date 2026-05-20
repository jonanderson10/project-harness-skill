# Audit Mode — Verify Harness is Current and Complete

**When:** You want to do a full check: What's current? What's stale? What's missing?

---

## How It Works

### Step 1: Compare Code Against Docs

Walk the folder structure and compare against `docs/TECHNICAL.md`:
- Check if directories and files match what's documented
- Look for new components not in `docs/DESIGN.md`
- Look for feature changes not in `docs/PRODUCT_SENSE.md`

### Step 2: Identify Gaps

- Missing decision logs (code shows GraphQL but no DECISIONS.md entry)
- Outdated sections (doc describes `src/api/` but code uses `src/services/`)
- Incomplete documentation (CLAUDE.md links to a doc that doesn't exist)

### Step 3: Generate Scored Report

**Scoring rubric (out of 10):**
- Start at 10
- Each stale section: -1
- Each missing core doc (CLAUDE.md, docs/TECHNICAL.md, docs/PRODUCT_SENSE.md): -2
- Each unlogged architectural decision found in code: -1
- Each broken/missing link for a referenced doc: -0.5

**Why these numbers?**
- Missing core docs (-2) are most impactful because they affect overall understanding
- Stale sections (-1) are common and fixable
- Unlogged decisions (-1) risk incorrect assumptions
- Broken links (-0.5) are minor but indicate drift

**Output format:**

```
Harness Audit — Score: 6/10
============================

✅ CURRENT
- CLAUDE.md
- docs/PRODUCT_SENSE.md
- docs/TECHNICAL.md (Project Structure section)
- docs/DECISIONS.md (5 recent entries)

⚠️ STALE  (-1 each)
- docs/DESIGN.md, Component Library section
  (You added DatePicker, Modal, Dropdown but not documented)
- docs/TECHNICAL.md, Data Model section
  (Schema changed 2 weeks ago, docs not updated)

❌ MISSING  (-1 to -2 each)
- Decision: Why did you switch from REST to GraphQL?
  (Code shows GraphQL but no decision logged)  [-1]
- docs/references/authentication.md
  (Auth strategy not documented; CLAUDE.md links to it but file missing)  [-2]

RECOMMENDATIONS (Priority Order)
1. Update docs/DESIGN.md Component Library (impacts context quality)
2. Log GraphQL decision (architectural context)
3. Update docs/TECHNICAL.md Data Model (enables accurate context)
4. Create auth reference doc + fix link in CLAUDE.md

Target: 9+/10 before starting a major feature
```

---

## What to Do With the Results

1. **Fix high-priority items immediately** — missing core docs, major architectural gaps
2. **Schedule low-priority items for next week** — stale sections, minor missing refs
3. **Defer "nice-to-have" stuff** — polish, additional detail

**Outcome:** Clear visibility into harness health. Know exactly what needs fixing.

---

## Running the Audit

You can run an audit by:
1. Invoking the skill in Audit mode: "Run an audit on the project harness"
2. Using the `/audit` slash command if `.claude/commands/audit.md` is set up

For deeper assistance (help fixing issues, guidance on updates), invoke the project-harness skill in **Maintain** mode after the audit.

---

## Audit vs. Maintain Spot-Check

| | Audit Mode | Maintain Spot-Check (Pattern C) |
|---|---|---|
| **Depth** | Full scored report | Quick scan |
| **Output** | Score, detailed findings, prioritized recommendations | List of obvious stale docs |
| **Time** | 5–10 minutes | 1–2 minutes |
| **When** | Periodic health check, before major features | During active development |
| **Best for** | Comprehensive overview | Fast check during workflow |