# Skill: Archive

**Trigger:** Something is confirmed inactive — a project finished or dropped, a person you've lost contact with, a goal abandoned, a resource gone stale.
**Goal:** Keep active surfaces clean without losing history.

## Rules
1. **Archive, never delete — object-wise.** Move the file to `99 System/Archive/<Type-plural>/` (no folder numbers): a project → `Archive/Projects/`, a resource → `Archive/Resources/`. Journal notes → `Archive/Journal/YYYY/YYYY-MM mmm/`.
2. **Update status first.** Set the object's type-specific status property (e.g. `project_status: done`/`dropped`) to its terminal value and add a dated line in the body: `- 2026-05-29 → archived, completed`.
3. **Lifecycle vs reference.** **Lifecycle objects** (`project`, `goal`) archive when they hit a terminal status — keep the active Projects folder to live work. **Reference/history objects** (`person`, `note`, `resource`, `event`) are *not* "completed"; archive only when genuinely dead. A dormant contact stays in People (set `relationship: dormant`) — never archive people lightly.
4. **Journal year-rollover.** When a year is complete, bundle that year's month folders into an annual folder and move it to `Archive/Journal/YYYY/` (→ `Archive/Journal/2026/2026-05 May/…`). Propose this in `vault-health`; move only on the user's nod (dailies are theirs to file).
5. **Keep links intact.** Archived objects still resolve as wikilinks — history and backlinks survive. Don't strip relations.
6. **Use the CLI** (`obsidian move …`) when Obsidian is running, so the index stays in sync; otherwise move the file directly.

Report what was archived in one line.
