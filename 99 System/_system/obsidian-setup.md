# Obsidian Setup

This vault is plain markdown — it works in any editor. These steps make Obsidian render the dashboards and tasks. All optional; nothing here is required for the data to be valid.

## 1. Open the vault
Obsidian → *Open folder as vault* → select the `Personal OS` folder.

## 2. Community plugins (Settings → Community plugins → Browse)

| Plugin | Why | Required? |
|--------|-----|-----------|
| **Dataview** | Powers every live dashboard in `@Dashboards/`. Without it, those notes show raw query code. | Strongly recommended |
| **Tasks** | Renders inline `- [ ]` checkboxes with due dates, priorities, and filtering. | Recommended |
| **Templater** *(or core Templates)* | Insert object templates from `99 System/Templates/` with one command. | Optional |
| **Terminal** *(by polyipseity)* | Run your AI CLI *inside* Obsidian, so you never leave the vault. | Optional |
| **Kanban** *(community)* | Drag-and-drop boards (e.g. Active Projects by status). | Optional — for boards |
| **Bases** *(core, recent Obsidian)* | Native database views — sortable/filterable tables & cards from note properties. Enable in Core plugins. | Optional — alt to Dataview tables |

The assistant builds your dashboards for you (the `build-dashboard` skill) using whichever of these are installed — it clarifies what you want to see, then creates it in `@Dashboards/`. You don't write any queries.

After enabling **Terminal**, open Settings → **Terminal** and set **Renderer → DOM** and **default profile → Integrated**. If output still looks garbled (`�`, broken boxes, smeared lines), just say so — the assistant runs `99 System/_system/skills/fix-terminal.md` and applies the right fix for your OS.

### Tasks: plugin or not? (you'll be asked at onboarding)
Tasks are plain `- [ ]` checkboxes either way. The Tasks plugin adds nicer rendering, editing, and reminders. You don't have to decide forever:
- **Yes** → `tasks_mode: tasks-plugin` — full rendering + reminders.
- **Not now** → `tasks_mode: dataview-only` (dashboards still work) or `plain` (no live queries).

**Changing your mind later is free.** Every task is written in the same format (`- [ ] … 📅 2026-06-02`) regardless of your choice, so to switch you just install the Tasks plugin and update `tasks_mode` in `99 System/_system/config.md` — **nothing to rewrite.** If you started in `plain` mode and never added dates, simply start adding `📅` dates going forward (the AI can backfill known ones).

After installing Dataview: Settings → Dataview → enable **"Enable JavaScript Queries"** is *not* needed; the standard `dataview` code blocks are enough.

### Core plugin: Daily Notes (only if you chose `daily-note` capture)
*Daily Notes* is a **core** plugin (built in — no download). Enable and configure it only if `capture_layer: daily-note` in `config.md`:
1. Settings → **Core plugins** → turn on **Daily notes**.
2. Settings → **Daily notes**: set **New file location** = your **Journal folder root** (e.g. `Journal`), **Date format** = `YYYY-MM-DD`.
New daily notes land flat in the Journal root. Daily notes need **no frontmatter** — the system knows they're dailies because they live in the Journal folder, and reads their date from the filename (using the format you set here). So you can change the date format anytime and nothing breaks. When the AI finishes processing one (via `/process-today`) it tags it `#ai-processed` and **leaves it there** — you then file it into the current month folder (`Journal/YYYY-MM mmm/`, e.g. `Journal/2026-05 May/`) at your own pace. At year-end, whole years get bundled into `Archive/Journal/YYYY/`. The AI never moves your dailies. (On `inbox` capture you can skip this whole step.)

## 3. Recommended core settings
- **Files & Links → Default location for new notes:** `00 Inbox/` (so quick-capture lands in the right place).
- **Files & Links → Default location for new attachments:** *In the folder specified below* → `99 System/Files` (keeps pasted images/PDFs out of your content folders).
- **Files & Links → New link format:** *Shortest path when possible*.
- **Files & Links → Use [[Wikilinks]]:** ON.
- **Appearance:** any theme; the vault is content-only and theme-agnostic.
- **Files & Links → Excluded files:** pre-set in `app.json` to `99 System/` (all machinery) and the regex `README\.md$` (every folder `_README` + the root readme), so they grey out and drop from Quick Switcher, graph, and link suggestions. This setting accepts **regex patterns**, so any file class can be de-emphasised this way. Note: Obsidian only *de-prioritises* excluded files in full-text search — greyed files can still appear there. To remove a subtree from search *entirely*, dot-prefix it (e.g. `.agent/`).

> **These are starting points, not commitments.** Change the daily-note folder/format, attachment location, or any of these anytime in Obsidian — **the OS reads your actual settings and follows them; there's nothing to update by hand.** (It treats `.obsidian/` as the source of truth; `vault-health` reconciles if you move existing files.) See `99 System/_system/config.md` → *Obsidian-owned settings*.

## 4. Mobile
Obsidian mobile opens the same Drive-synced folder. Capture on the go into `00 Inbox/`; triage later. (Note: keep Google Drive's offline sync on for this folder so mobile and desktop stay consistent.)

## 5. Let your AI operate the vault directly (the `obsidian` CLI)

For the AI to manage your OS with full leverage — creating notes from templates, setting properties, searching, moving files — it uses the official **`obsidian` command-line tool**. This keeps Obsidian's index and plugins in sync, which raw file edits don't. You don't type any of these commands; the AI does. You just need to enable it once.

**Non-technical setup — three one-time steps:**
1. **Open the vault in Obsidian** (step 1 above). This registers the vault under the name **`Personal OS`**, which is how the AI addresses it.
2. **Keep Obsidian running** while you work with the AI. The CLI talks to the live app — if Obsidian is closed, commands fail and the AI falls back to editing files directly (still works, just less tidy).
3. **Install the CLI if your AI says it's missing.** If the AI reports the `obsidian` command isn't found, ask it: *"install the Obsidian CLI and walk me through it."* It will give you the exact copy-paste steps for your computer. Nothing here requires you to understand the command line — you only paste what the AI hands you.

> If you ever see the AI ask you to "open Obsidian first," that's this CLI needing the app running. Open it, and continue.

## 6. If you don't use Obsidian
Everything still works as plain markdown in VS Code or any editor. You lose live dashboards — the `@Dashboards/` notes become hand-maintained index lists instead of auto-updating queries. The AI operator can refresh them on request.
