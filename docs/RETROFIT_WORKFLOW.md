# Retrofit Mode — Full Workflow Example

This is a reference document showing the complete Retrofit workflow. See [docs/RETROFIT.md](docs/RETROFIT.md) for the full mode documentation.

---

## Example: Full Retrofit Workflow

```
You: "Create a harness for this existing project"

Skill: [scans codebase for 30 seconds]
       "I see a Node.js + React app, using GraphQL, with PostgreSQL backend.
        Let me ask you some questions to understand it better."

Phase 1: Product & Purpose
Skill: "What is this? I see dashboards and data export. Is that the full scope?"
You: "Yes, it's an analytics dashboard for internal use."
Skill: "Who uses it?"
You: "Data team and PMs. Maybe 50 active users."
Skill: [continues through Phase 1]

Phase 2: Technical Architecture
Skill: "Why GraphQL? What alternatives did you consider?"
You: "REST was the original plan, but we switched to GraphQL because we needed flexibility on the frontend."
Skill: [asks about data model, deployment, integrations, testing, etc.]

Phase 3: Key Decisions
Skill: "What were your biggest architectural decisions?"
You: "Decided to keep frontend and backend tightly coupled in one repo.
       Used GraphQL subscriptions for real-time updates.
       Built a custom auth system instead of using Auth0."
Skill: [asks about trade-offs, constraints, core beliefs, etc.]

Phase 4: UX & Design
Skill: "Walk me through the primary user journey"
You: [explains how someone logs in, views metrics, exports data]
Skill: "Any design guidelines? Colors, typography?"
You: [describes the design system]

Phase 5: Codebase Map
Skill: "Walk me through the folder structure"
You: [explains src/components, src/pages, src/api, etc.]
Skill: "How do developers add new features?"
You: [explains the workflow]

Phase 6: Missing Context
Skill: "Any gotchas?"
You: "The GraphQL subscriptions are flaky under high load. We know it needs work."
Skill: [asks about deployment, security, roadmap, etc.]

Phase 7: Generate Harness
Skill: [generates CLAUDE.md, PRODUCT_SENSE.md, DESIGN.md, TECHNICAL.md, DECISIONS.md]

Phase 8: Review & Refine
You: [reviews generated docs]
     "This is 90% right. Let me fix these 3 things and add more detail about the custom auth."
Skill: [adjusts]
You: "Perfect. Commit it."
```

**Outcome:** Your 6-month-old codebase now has complete harness docs. Ready for any agent to work on it.