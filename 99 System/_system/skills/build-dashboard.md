# Skill: Build Dashboard

**Invoke:** `/dashboard`
**Trigger:** The user **explicitly asks** to see something ("show me active projects", "a board of my tasks", "a Today list"), or picks from a proposed starter set at onboarding.
**Goal:** **Clarify what the user wants, then build exactly that** — no more — as a `view` note in the right folder, using the best available tool, reading from the live object graph (never duplicating data).

## ⚠️ Build only what's asked — never bulk-build
**Do not create a pile of views the user didn't request.** Clutter is a failure. Rules:
- Build **only** the specific views the user explicitly chose. If they chose none, build none.
- **Propose, then wait.** Offer options as a short list; build only the ones they pick.
- When unsure, build **at most one** (a single Home) and ask before adding any more.
- Per-Area dashboards already exist (every area note is one) — don't duplicate them as separate views.

## Two homes — keep tasks separate from dashboards
- **`@Tasks/`** — task **smart-lists** (Today, Upcoming, Open, Done, By Area/Project). This is the user's task-manager surface, like Todoist/TickTick/Things — each list is a `view`. Tasks live separately from dashboards so they're easy to find.
- **`@Dashboards/`** — everything else: overview/Home, project boards, custom rollups.
Both folders are `@`-prefixed so they sit at the top of the file list. Create a folder only when its first view is actually built.

## Step 1 — Clarify what they want (always first)
Ask, plainly, and reflect back before building:
- **What** — tasks, projects, people, a custom type?
- **Filter** — only open? this Area? due this week? a tag?
- **Shape** — a simple list, a sortable table, or a board grouped by status/stage?
- **Sort/group** — by due date? Area? stage?
Confirm in one line: *"So: a board of active projects grouped by status — right?"* Then build that one thing.

## Step 2 — See what's installed (verify, don't assume)
**Read `.obsidian/community-plugins.json` and `core-plugins.json`** to see what's actually enabled — never claim a plugin is present without checking:
- **Dataview** — queries → lists/tables (the default).
- **Bases** — native database views (table/cards, filter/sort on properties).
- **Kanban** — drag-and-drop boards.
If none are installed, say so and build a hand-maintained list (or offer to help install one).

## Step 3 — Pick the renderer → tool (shape decides)
| Shape | Build with |
|-------|-----------|
| List / filtered list (open tasks, due-this-week) | Dataview (or Bases) |
| Sortable/filterable table | Bases if present; else Dataview TABLE |
| Board grouped by status/stage | Kanban if present; fallback = Dataview grouped list |
| Pinned / key notes | query on `pinned: true` |
| Nothing installed | hand-maintained list the assistant refreshes |

## Step 4 — Build it & explain
- Create the `view` note (`type: view`) in **`@Tasks/`** (task smart-list) or **`@Dashboards/`** (everything else). Name it for what it shows.
- One plain line: what it shows, that it updates itself.
- **Pins:** "pinned" is a queryable **property** (`pinned: true`), not Obsidian's per-pane pin.

## Starter set (only at onboarding; propose, build only what's picked)
Offer — don't build unprompted: a **Home** dashboard; a couple of **task smart-lists** (Today, Open) in `@Tasks/`. That's plenty to start; more on request.
