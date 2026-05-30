# Skill: Onboarding Interview

**Invoke:** auto — runs on the user's **first message** to an un-onboarded vault (even "hi").
**Trigger:** `99 System/_system/onboarding-state.md` is missing or `status: not-started`.
**Goal:** A short, friendly interview that learns the user's life, then builds their personalized OS. Keep it **tight and crystal clear** — at every step the user knows what you're asking and why.

## Non-negotiables (read before you start)
- **Treat the user as unknown.** Ignore any name/company/role you might know from elsewhere. Greet neutrally; **never use a name they haven't given you here**; use only generic examples. Discover everything by asking.
- **Reflect & reassure.** Play back what they say in one line; let them confirm or fix. They can't get it "wrong" — it sharpens with use.
- **Educate plainly.** Explain each idea in one jargon-free sentence as it appears ("Areas are the big parts of your life"; "you dump thoughts in one place and I file them"). If they're new to Obsidian, give the 2-line basics first ("it's just a folder of notes on your computer; you mostly talk to me; you can't break anything").
- **Verify, never claim.** Before saying a plugin/setting is on, actually read `.obsidian/community-plugins.json` / `core-plugins.json`. If unsure, say so.
- **Minimalism.** Before any new type, check it isn't just a field/relation on an existing one. A few solid types beat many thin ones — anything can be added later.
- **One question at a time**, ~7 exchanges. If they say **"skip,"** build the Core-set fallback (types: Person, Note, Event, Project, Task, Resource — Areas: Health, Finances, Relationships, Career, Learning, Home) and finish.

## Quick setup check (do this FIRST, before building anything)
- **Verify the `obsidian` CLI and that Obsidian is running** — actually run a check (e.g. `obsidian --version` / list vaults). This decides *how* you'll build the vault below: via the CLI (preferred — keeps the index/links in sync) or direct file writes (fallback). **Don't skip this and default to raw file edits.** State which mode you're in.
  - CLI present + Obsidian open → use it for creating notes/objects/areas.
  - CLI missing → offer the one-copy-paste setup ("a small helper so I can configure things for you"); meanwhile proceed with direct writes and tell the user.
- Note which view plugins are actually installed (verified by reading `.obsidian/community-plugins.json` / `core-plugins.json` — never assume).

## The interview — tight flow (~7 questions)
1. **You.** "First — your name, and what you spend your days on?" (and the rough shape of your week). → `owner.md`.
2. **Your areas.** "What are the big areas of your life and work?" Nudge with **generic** examples only (Health, Work, Finances, Family, Learning, Home) — never a real company/project name.
3. **What you track.** Propose the universal set — **Person · Note · Event · Project · Task · Resource** — one line each ("a Person = one note per person you know"); they keep / drop / rename. Then: "Anything else you keep track of?" For each custom thing, reflect in a line **and how it connects** to others (a `client` links to a company + projects). If they decline a touchpoint type (events/meetings), ask how to handle it instead — its own records, or lines in the daily note with links — and record that choice.
4. **Capture.** "When a thought hits — drop it in a quick **Inbox**, or jot it into **today's note**?" → `capture_layer`.
5. **See at a glance.** "Want a **Home** view and a **Today/Open** task list?" Build only what they pick — nothing more.
6. **A few quick choices** (bundle in one breath, all changeable later): use the **Tasks** plugin for reminders? **Live dashboards** (Dataview)? **Name your assistant** (default *Grove*)?
7. **Your voice.** "Paste a line you'd write to yourself (or point me at 2–3 notes) so I match your style." → `writing-style.md`.

*(One vault by default — only discuss splitting if they raise a real privacy/sharing need. Offer importing existing notes at the very end, not now.)*

## Build it (instantiate — only for what they kept)
The vault ships with just `00 Inbox/` and `99 System/` (and `99 System/Templates/` is **empty**). Use the **`obsidian` CLI** for creating notes/objects when it's available (per the setup check); fall back to direct writes only if Obsidian is closed/CLI missing. Create the rest now:

1. **A home folder + a template for EVERY kept type.**
   - Folder = the **plural** of the singular type (`note`→`Notes/`, `project`→`Projects/`), each with a one-line `_README`.
   - **Number folders by FREQUENCY — most-used on top** (e.g. `10 Projects`, `20 People`, `30 Notes`, `40 Areas`, `50 Journal`, `60 Resources`). Pick the order to fit *this* user. **If they chose `daily-note` capture, put the Journal folder right after `00 Inbox`** (e.g. `05 Journal`) — it's the daily capture surface they touch most.
   - **Populate `99 System/Templates/`** with one template per kept type: **copy each kept type's pattern from `99 System/_system/template-library/`** into `Templates/`, and **generate a fresh template for each custom type** (minimal fields, no `title` field — the filename is the title). Only kept types — never copy the whole library.
   - Create one `area` note per domain from the `area` template; each area note is its own dashboard.
2. **Registries:** update `object-types.md` (types + a **recognition signature** per type), `relations.md` + `object-model.canvas` (the connections), `config.md` (`tasks_mode`, `dataview`, `capture_layer`), `writing-style.md`, and the assistant name in `_agent/identity.md`. Record any "declined type → handle this way" rule in `classification-learnings.md`. **Register property types** for the kept types' properties in `.obsidian/types.json` (dates → `date`, controlled multi-value sets → `multitext`; edit the file directly — **never `property:set type=`**; see `properties-and-tags.md`). **List each controlled property's allowed values in `PROPERTIES.md`** (e.g. `project_status`, `area_status`, any custom enum) so values stay consistent. If `capture_layer: daily-note`, ensure the Journal folder exists and tell the user to enable the *Daily Notes* core plugin.
3. **Views:** build only the 1–3 the user picked (dashboards → `@Dashboards/`, task lists → `@Tasks/`) via `build-dashboard`. None if they picked none. Never bulk-build.
4. **Seed a few linked objects** (a couple of people, one active project), linked per `link-objects`, so the graph works from note one.
5. **Finish:** set `onboarding-state.md` to `status: complete`, `personalized: true`, with a one-paragraph summary; **move `START HERE.md` → `99 System/Archive/`**. Show the user their structure in 5–6 lines + one first action ("drop a thought in `00 Inbox/`"). Then offer importing existing notes (via `import-existing`) as the optional next step.
