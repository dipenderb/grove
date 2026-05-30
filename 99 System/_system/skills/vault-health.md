# Skill: Vault Health

**Trigger:** Periodically (monthly, or on request: "check my OS"). The maintenance pass that keeps the system from rotting.
**Goal:** Catch drift, sprawl, and orphans early — and propose fixes, not just flag them.

## Checks

1. **Inbox backlog.** Count un-triaged items in `00 Inbox/`. If piling up, offer to triage now.
2. **Orphans.** Objects with no links in *or* out (no `area`, no relations, no backlinks). Propose linking or archiving.
3. **Stale projects.** `project_status: active` projects untouched > 30 days. Surface them: still active, or archive?
4. **Active-folder hygiene.** Lifecycle objects at a terminal status still sitting in their active folder — `project_status: done`/`dropped` in the Projects folder (or `goal` achieved/abandoned) → propose moving to `Archive/<Type>/` so active surfaces show only live work.
5. **Journal year-rollover.** Month folders from a *completed prior year* still in the active Journal → propose bundling them into `Archive/Journal/YYYY/`. Also: daily notes lingering untagged in the Journal root (need `/process-today`).
6. **Broken intent.** Unresolved `[[wikilinks]]` that look like they *should* exist (recurring stubs) — propose creating them.
7. **Duplicate people.** Same person under two filenames (nicknames, spellings). Propose a merge.
8. **Type-sprawl audit.** Re-run the 4-criteria test (`architecture.md`) on every custom type in `object-types.md`. Any type with < 3 instances after months, or that now reads as "a kind of [other type]," is a merge candidate. **This is the anti-Salesforce-rot check** — do it honestly.
9. **Property & tag sprawl.** Frontmatter fields no View queries → demote to body prose. Tags used on only one or two notes, tags not in the `properties-and-tags.md` allow-list, or near-synonym tags (`#health`/`#wellness`) → propose prune/merge. Flag any value duplicated across a link *and* a tag/property (violates one-fact-one-place).
10. **Controlled-value drift.** For each property in `PROPERTIES.md`, find note values **not** in its allowed set (`Activ`/`in progress` vs `active`) → propose normalising. Allowed values used by no note → prune from `PROPERTIES.md`. Check each controlled property's type in `.obsidian/types.json` is registered (single→`text`, multi→`multitext`).
11. **Promotion review.** Read `classification-learnings.md` → promote consistently-held learned rules into the default signal table.
12. **Object-model sync.** Check `object-model.canvas` against `object-types.md` and `relations.md`: every active type should be a node, every relation a labelled edge. Flag missing/stale nodes or edges.
13. **README & attachment hygiene.** Folder READMEs still describe the right *purpose/conventions* (not contents) → fix stale-purpose ones. Attachments in the attachment folder referenced by no note → orphan candidates to archive.
14. **Obsidian config drift.** Read `.obsidian/` (daily-notes folder/format, `app.json` attachment/new-note location, enabled plugins) and reconcile: if the user changed a setting, update any OS references that assumed the old value, and offer to consolidate notes/attachments left in the old location (Obsidian doesn't move existing files when a setting changes). The live `.obsidian/` values win — never overwrite them to match the OS.
15. **Portability.** Verify the OS stays self-contained: no absolute paths in objects or config, all wikilinks/relative links resolve, and the attachment folder is **inside** the vault. Flag anything that would break if the user moved the folder elsewhere.

## Output
A short report: what's healthy, what's drifting, and a numbered list of proposed cleanups for the user to approve. Don't auto-delete or auto-merge — propose, then act on approval.
