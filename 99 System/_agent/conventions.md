---
type: agent-convention
updated: 2026-05-29
---
# Agent Workspace Conventions

How I keep my own workspace fast, lean, and clean. Same discipline I apply to the human vault — applied to myself.

## Atomicity · modularity · interconnection
The OS principles (`../_system/principles.md`), applied to my own files: one concept per file; reference by path/`[[link]]`, never duplicate; link related files so context is one hop away.

## Frontmatter-first (fast search, low tokens)
Every file leads with frontmatter carrying the decision-relevant fields, so I can **scan frontmatter to find the right file without reading bodies**:
- `type:` — `agent-index` · `agent-identity` · `agent-convention` · `agent-log` · `agent-memory`
- `updated:` — ISO date
- `tags:` — few, from a small set
- `refs:` — paths/links this file depends on

Search order: filter by `type`/`tags`/`updated` in frontmatter → open a body only when the frontmatter says it's relevant.

## Naming = the key
- Logs: `logs/YYYY-MM-DD.md`
- Memory: `memory/<kebab-topic>.md` — one topic per file; the filename tells me what's inside without opening it.

## No duplication
- Vault-content learnings live in `../_system/` (classification → `classification-learnings.md`; voice → `writing-style.md`). I **link**, never copy.
- `AGENT.md` and this file are index/spec — they reference, they don't restate.

## Stay out of the human's views
- Use **plain `-` bullets**, never `- [ ]` task checkboxes, in my files — so my work never appears in the human's task dashboards. The human's Views are folder-scoped to `00`–`99` and already exclude `99 System/_agent/`.

## Reading the user's vault
- The user edits their vault continuously. **Always re-read the relevant notes/folders live** (CLI / file / Dataview) before acting or advising — never rely on stale session memory or on my own memory notes for the user's current content. The disk is the truth.
- My `memory/` holds *operating patterns* (how the user works, my failure modes), **never copies of the user's vault contents** — those are read live each time.

## Token efficiency (my design rule)
- Entry point (`AGENT.md`) is a small index; load atomic files on demand.
- Every file short and single-purpose. Prefer a link over inlined context.
- Prune stale memory and old logs during `vault-health`.
