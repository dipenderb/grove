# Conventions

Mechanical rules that keep the vault consistent and queryable. When in doubt, match what already exists.

## Type & folder naming
- **Type names are singular; folder names are plural.** The object *type* is singular (`person`, `project`, `gig`); the *folder* that holds its notes is the plural form (`People/`, `Projects/`, `Gigs/`). This is the standard for every type — default or custom.
- **One note = one instance.** Each note in the folder represents a single thing — one person, one project, one gig.
- When a type's home folder is created (at onboarding or via `new-object-type`), pluralise the type name for the folder.
- **Number folders by frequency of use** — the most-frequently-opened types get the lowest numbers so they sit on top (e.g. `10 Projects` above `40 Areas`). Numbers are sort-order only; reorder anytime as habits change. (`@Dashboards`/`@Tasks` use `@` to sit above all numbers; `99 System/` stays at the bottom.)
- **Templates** live in `99 System/Templates/` — one per object type **the user keeps**, created at onboarding (and by `new-object-type`). `Templates/` ships **empty**; templates are generated there from the reference patterns in `99 System/_system/template-library/`. Never pre-ship templates for types the user hasn't kept.

## Files & naming
- One object = one file. Filename = the object's title (human-readable, spaces allowed): `Priya Nair.md`, `Renovate kitchen.md`.
- **No `title` frontmatter field.** The filename *is* the title — Obsidian renders it as the note's H1. A separate `title:` duplicates it and goes stale the moment the file is renamed. To rename an object, rename the file (Obsidian updates inbound `[[links]]` automatically).
- People: filename = the name you actually call them (`Priya`, or `Priya Nair` if that's how you refer to them) in the People folder. Put the formal name in the `full_name` field when it differs from the filename. Disambiguate clashes by adding context (`Priya (vet)`).
- **Journal structure.** The Daily Notes plugin creates each daily note **flat in the Journal folder root** (`YYYY-MM-DD.md`) — resolve the actual folder + date format from `.obsidian/daily-notes.json`, never hardcode the number. The **active** Journal holds **month folders directly** (`Journal/YYYY-MM mmm/`, e.g. `Journal/2026-05 May/`). After `/process-today` tags a note `#ai-processed`, **the human** files it into the right month folder — **the agent never auto-moves dailies.** At **year rollover**, that year's month folders are bundled into an annual folder and moved to `Archive/Journal/YYYY/` (→ `Archive/Journal/2026/2026-05 May/…`), keeping the active Journal to the current period. Weekly notes: `Journal/Weekly/YYYY-Www.md` (e.g. `2026-W22.md`).
- Captures: `00 Inbox/YYYY-MM-DD HHMM <slug>.md`.

## Frontmatter
- Always YAML, always at the top, fenced by `---`.
- Required on every **object**: `type`, `created`.
- **Order properties most-glanceable first; housekeeping last.** Top → bottom: **status** (`*_status`, if the type has one) → **key attributes & relations** (identity like `full_name`, then `area`, dates like `due`/`date`, links like `with`/`org`, `role`, `outcome`, `url`…) → **`tags`** → **`type`** (second-last — it's a discriminator, not something you read) → **`created`** (last — pure metadata). Apply this in every template and whenever you add a field or a new type.
- **Exception — journal notes (daily/weekly) carry no required frontmatter.** They're identified by living in the Journal folder (daily) / `Journal/Weekly/` (weekly), and their date/week comes from the filename. Keeps the capture surface clutter-free.
- **Why `type` when folders already group by type?** The folder is a *view*; `type` is the *fact*. Folders are numbered by frequency and **renumbered as habits change** (`30 Projects`→`10 Projects`), and objects move to `99 System/Archive/` — so path-based identity is fragile. `type` is stable: Dataview uses `WHERE type = "project"` (works across renumbering + archive), captures in `00 Inbox/` get typed *before* they have a folder, and the classifier's decision stays explicit and correctable. This is not the duplication the no-duplication rule forbids (that's about copying *facts/content*).
- Wikilinks inside frontmatter must be quoted: `area: "[[Health]]"`. Lists of links use YAML list syntax.
- Dates are ISO: `YYYY-MM-DD`. Datetimes: `YYYY-MM-DD HH:MM`. Never locale formats.

## Dates
- Run `date` before writing any timestamp. Never estimate.
- Relative references ("next Friday", "yesterday") get resolved to an absolute date at write time.

## Linking
- Connect with `[[wikilinks]]`. Link the canonical object (the file), not a copy of its content.
- A link to a not-yet-created object is fine — it marks a stub worth creating later. Obsidian shows it as an unresolved link.
- Prefer linking over restating. If you find yourself copying a fact, link the source instead.

## Properties & tags
- The full discipline — when to use a link vs. property vs. tag, the no-duplication rule, and how to keep the set small — lives in `99 System/_system/properties-and-tags.md`. Don't restate it here; follow it there.

## Attachments
- Binary attachments (pasted images, PDFs, voice notes) default to `99 System/Files/`. Set Obsidian's default attachment location there (see `obsidian-setup.md`).
- An attachment is raw storage, embedded via `![[file]]`. To *track* a file as an object (with metadata/links), create a `resource` in the Resources folder that points to it. Don't confuse the binary (in `99 System/Files/`) with the tracked object.

## READMEs
- A folder README describes the folder's **purpose and conventions** (what belongs here, how it's named) — **never a list of current contents**, which goes stale instantly. Live contents come from reading the vault. Update a README only when the folder's *role* changes.

## Archiving
- **Active folders hold active items; the Archive holds inactive ones — organised object-wise** (no frequency numbers): `99 System/Archive/<Type-plural>/` (e.g. `Archive/Projects/`, `Archive/Resources/`).
- **Lifecycle objects archive on a terminal status:** a `project` that's `done`/`dropped` (and any `goal` that's `achieved`/`abandoned`) moves out of its active folder into `Archive/<Type>/`, so the active surface shows only live work. **Reference/history objects stay** — `person`, `note`, `resource`, `event` aren't "completed"; archive them only when genuinely dead/irrelevant (a dormant contact stays in People).
- **Journal archives by year:** `99 System/Archive/Journal/YYYY/YYYY-MM mmm/` (see the Journal structure note above).
- **Never delete** — links stay intact (Obsidian resolves wikilinks across folders, including Archive).

## Status & timestamps on change
- When you change an object's status property (e.g. `project_status`, `area_status`), note it in the body with a dated line: `- 2026-05-29 → moved to active`.
