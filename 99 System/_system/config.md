---
type: os-config
updated: 2026-05-29
capture_layer: inbox
tasks_mode: tasks-plugin
dataview: true
---
# OS Config

Runtime choices, set at onboarding, changeable anytime. Atomic — the OS's switches live here, not scattered.

> Status: **DEFAULT (not yet personalized)** — the frontmatter values above are seed defaults; onboarding sets the real ones. Replace this line with `PERSONALIZED — YYYY-MM-DD` after onboarding.

## capture_layer — where quick captures land
- `inbox` *(default)* — each quick capture is a file in `00 Inbox/`, triaged into objects. Clean separation of "unprocessed" from "filed."
- `daily-note` — captures are appended to **today's daily note**; the `process-daily-note` skill (`/process-today`) segments the day's log into blocks and files each into objects, then tags the note `#ai-processed`. Suits people who think in a running daily log. **Requires the Obsidian *Daily Notes* core plugin**; its folder and date format are **Obsidian-owned** (we suggest the **Journal folder root** + `YYYY-MM-DD` at setup, but the OS follows whatever you actually set — see below).

Either way, `00 Inbox/` still exists as the intake for external channels (email-forward, etc.) and triage still files everything into objects. Switching later just changes where new captures go — nothing already filed moves.

## Obsidian-owned settings — read live, never duplicated here
Some settings belong to Obsidian, not the OS. **The OS reads them live from the vault's `.obsidian/` config (or via the `obsidian` CLI, which respects them) and follows whatever the user set — it never hardcodes or copies these values.** If the user changes one in Obsidian, the OS just adapts; there is nothing to update here.

| Setting | Source of truth | OS suggests at setup |
|---------|-----------------|----------------------|
| Daily-note folder & date format | `.obsidian/daily-notes.json` (`folder`, `format`) | Journal folder root, `YYYY-MM-DD` (human files into `Journal/YYYY-MM mmm/`; past years → `Archive/Journal/YYYY/`) |
| Default attachment location | `.obsidian/app.json` (`attachmentFolderPath`) | `99 System/Files` |
| Default new-note location | `.obsidian/app.json` (`newFileLocation`) | `00 Inbox` |
| Link format / wikilinks | `.obsidian/app.json` | shortest path, wikilinks on |
| Enabled core/community plugins | `.obsidian/core-plugins.json`, `community-plugins.json` | Daily Notes (if `daily-note`), Dataview, Tasks |
| Property **type** registry (text/list/date per property) | `.obsidian/types.json` | `created`/`due`/`date`=`date`, `tags`=`tags`; controlled multi-value sets=`multitext` |

**Rule:** before reading or writing a daily note (or resolving an attachment path), resolve the actual folder/format from `.obsidian/` — or just use `obsidian daily:read` / `daily:append`, which already honor the user's settings. Never assume a literal path or date format. If there's no `.obsidian/` (not using Obsidian), fall back to the suggested defaults. `vault-health` reconciles any drift.

**The daily-note date format can change anytime — this must never break the system.** Daily notes carry **no identifying frontmatter** — they're identified by **location (inside the Journal folder, resolved live from `.obsidian/daily-notes.json`)**. Get a note's date by parsing its filename with the live `format` from that same config (Dataview's `file.day` does this automatically). So switching `YYYY-MM-DD` → `DD-MM-YYYY` (or any format) changes only filenames; identification (folder) and date-parsing (live format) keep working — nothing date-related is stored on the note.

**Property types:** register a property's type by editing `.obsidian/types.json` directly (e.g. `"<prop>": "multitext"` for a List). **Never** `obsidian property:set type=…` — it corrupts the note. Full rule + the Text/List/Date decision in `properties-and-tags.md`.

**Portability note:** keep the attachment folder **inside the vault** (default `99 System/Files`). Pointing it to a folder outside the vault breaks self-containment — the OS would no longer move cleanly as one folder. If the user sets it outside, flag it in `vault-health`.

## tasks_mode — how tasks are tracked & queried
**All modes use the same task line format** (below), so changing mode **never requires rewriting any task.**

- `tasks-plugin` *(recommended)* — Tasks plugin installed: rich rendering, inline editing, natural-language queries.
- `dataview-only` — no Tasks plugin, but Dataview installed: dashboards still work (Dataview reads the date emoji).
- `plain` — no query plugins: plain checkboxes, dashboards maintained by the AI / by hand.

## Canonical task line (mode-independent)
```
- [ ] Call the bank 📅 2026-06-02 ⏫
```
`📅` due · `⏳` scheduled · `🛫` start · `🔼/⏫/🔽` priority · `✅` done date.

Why this format is safe in every mode: it's readable plain text with **no** plugin; **Dataview** parses the date emoji (`📅 ⏳ ✅`) into queryable fields; the **Tasks plugin** parses all of it. This is what makes "start without the plugin, add it later" a free switch.

## dataview — self-updating dashboards
- `true` *(recommended)* — Views in `@Dashboards/` are **live Dataview queries generated from the relationship model** (`relations.md` / `object-model.canvas`). Define the model once and dashboards stay current automatically: each Area lists its own people/projects, each person shows their timeline, overdue tasks surface on their own. **No manual list maintenance.**
- `false` — Views are hand-maintained index lists the AI refreshes on request.

Enabling it later is free: install Dataview, set this to `true`, and the AI generates the queries. The data (objects + links) doesn't change — only how it's displayed.

## Changing tasks_mode later
See `99 System/_system/obsidian-setup.md` → "Changing your mind about Tasks." Because the line format is constant, switching is: install (or remove) the plugin, update `tasks_mode` here. No data migration. If you were on `plain` and never recorded dates, just start adding `📅` dates going forward — the AI can backfill known ones on request.
