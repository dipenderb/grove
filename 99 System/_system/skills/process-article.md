# Skill: Process Article

**Invoke:** `/process-article`
**Trigger:** A captured **article / web-page link** — or invoked by `process-daily-note` / `capture-triage` when one is detected.
**Goal:** Turn a link into a useful, linked `resource` — not a raw URL.

## Steps
1. **Fetch** the article — *delegated* to a web tool / background agent (the orchestrator routes, doesn't fetch inline).
2. Create a `resource` (subtype `article`) with `url`, source, and **your takeaways in the user's voice** — a few lines, not a full copy (link, don't duplicate).
3. **Link** objects it relates to (people, projects, areas) per `link-objects`; set `area`.
4. If it implies an action, add an inline `- [ ]` task.

Report what was saved and where.
