Run a harness audit on this project.

1. Compare the folder structure against TECHNICAL.md
2. Check for new components or features not reflected in PRODUCT_SENSE.md or DESIGN.md
3. Scan git log for recent commits that suggest undocumented decisions
4. Check all relative links in CLAUDE.md resolve to existing files

Score the harness out of 10 using this rubric:
- Start at 10
- Each stale doc section: -1
- Each missing core doc: -2
- Each unlogged architectural decision found in code: -1
- Each broken link: -0.5

Output: score, current / stale / missing sections, prioritized fix list.

For a deeper audit, invoke the project-harness skill in Audit mode.