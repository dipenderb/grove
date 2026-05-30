# Skill: Daily Note

**Invoke:** `/today`
**Trigger:** User starts a day, or asks "what's today / plan my day."
**Goal:** A single dated note that orients the day and captures it as it happens.

> If `capture_layer: daily-note` (see `config.md`), this note is also the **capture surface** — the Log section is where quick captures land, processed by `process-daily-note`. **Role: a durable running log** — unlike the `00 Inbox/` queue (which empties), the daily note **stays** as the day's record; processing *enriches* it (objects extracted, mentions wikilinked), it doesn't empty it. Requires Obsidian's *Daily Notes* core plugin.

**Resolve the path/format from Obsidian, don't assume it.** The daily-note folder and date format are Obsidian-owned (`.obsidian/daily-notes.json`). Prefer `obsidian daily:read` / `daily:append` (they honor the user's settings), or read the folder/format from config before composing a filename. Don't hardcode a path — the suggested default is the Journal folder root, `YYYY-MM-DD.md` (the human later files processed dailies into the active month folder `Journal/YYYY-MM mmm/`, and past years bundle into `Archive/Journal/YYYY/`; you never move them).

## Steps
1. Run `date`. Target: today's daily note (folder/format resolved from Obsidian). If it exists, open and append — never overwrite.
2. If new, create it with **no identifying frontmatter at all** — a daily note is identified by **living in the Journal folder** (resolved from `.obsidian/daily-notes.json`), not by a `type` or `date` property. The date comes from the filename (read the `format` from config when you need to parse it; Dataview's `file.day` infers it too). This keeps the note clutter-free.
3. Populate the orientation block:
   - **Today's events** — query/scan `event` objects with today's `date`.
   - **Tasks due/scheduled today** — inline tasks with 📅 or ⏳ today (Tasks plugin surfaces these; otherwise scan).
   - **Open from yesterday** — uncompleted tasks rolled forward.
4. Leave a **Log** section for the user to capture through the day; treat anything they add as a mini-capture (link people/projects).
5. At day's end (or next morning), pull any loose threads into proper objects and roll incomplete tasks forward.

## Template
```markdown
## Focus
- 

## Today
- Events: 
- Due: 

## Log

## Carried forward
```
**No frontmatter** — identity is the Journal folder, the date is the filename. (`/process-today` adds the `#ai-processed` tag once processed; that's the only thing ever added.) Keep it light: a working surface, not an archive — durable facts graduate into typed objects.
