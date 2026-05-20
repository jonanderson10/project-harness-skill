# Maintain Mode — Keep Harness Current as Code Evolves

**When:** You're actively developing a harness-based project.

---

## Pattern A: After Making Code Changes

```
You: "I refactored the component folder structure"

Skill: [checks relevant docs]
       "TECHNICAL.md describes the old layout. Should I update it?"

You: "Yes"

Skill: [updates TECHNICAL.md with new structure]
     "Committed. Want to review?"

You: [reviews]
     "Looks good"
```

**When to use:** After any significant code change (new feature, refactor, structural change).

---

## Pattern B: After Making a Decision

```
You: "We decided to use GraphQL for the API"

Skill: [asks for context]
       "Why GraphQL? What alternatives did you consider?"

You: [explains]

Skill: [adds to docs/DECISIONS.md with full context]

You: "Commit it"
```

**When to use:** After any architectural decision, tech choice, or strategic shift.

---

## Pattern C: You Ask for a Health Check

```
You: "Are the docs still accurate? Spot check."

Skill: [scans code vs docs]
       "TECHNICAL.md still accurate. DESIGN.md missing 2 new components.
        Should I update it?"

You: "Yes"
```

**When to use:** During active development, when you want a quick check without running a full audit.

**Note:** For a full scored audit with prioritized recommendations, use **Audit Mode** instead. Pattern C is for quick spot-checks during active development; Audit Mode is for comprehensive health checks.

---

## General Guidelines

### When to Update Docs

- After any structural code change (new folders, renamed modules, moved files)
- After any tech decision (new dependencies, changed architecture)
- After any scope change (new features, removed features)
- Before starting a major feature (ensure docs reflect current state)

### How to Update

1. Check which docs are affected by the change
2. Identify what specifically changed
3. Update the doc with the new reality
4. Review before committing

### Context Cost

Aim to keep total loaded context (CLAUDE.md + all imported docs) under ~500 lines for optimal performance. If a doc exceeds 300 lines, consider splitting it.

---

## Empty or Stale CLAUDE.md

If `CLAUDE.md` exists but is empty or clearly stale (references old project names, missing files linked in it), treat the situation as a **Retrofit** — the harness needs to be rebuilt or significantly refreshed.

---

## Ownership

Assign a harness owner who reviews docs quarterly. In CLAUDE.md, you can add:

```markdown
<!---
owner: @username
lastReview: 2026-01-15
-->
```

This helps track who is responsible for keeping the harness current.

---

## Rollback

Before updating a doc, note its current state (copy the content, or use `git diff`). If the next agent session reports confusion after the update, revert to the previous version.

---

## Summary: Maintain Triggers

| Trigger | Action |
|---------|--------|
| Code structural change | Update TECHNICAL.md |
| New feature or scope change | Update PRODUCT_SENSE.md |
| Visual/UX change | Update DESIGN.md |
| Tech decision | Log in DECISIONS.md |
| New component library | Update DESIGN.md |
| Gotcha discovered | Add to relevant doc |
| Security/compliance change | Update relevant doc + DECISIONS.md |