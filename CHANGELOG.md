# Changelog

All notable changes to Grove. Versions use `vYY.MM.DD-build`. Updates are **CORE-only and backward-compatible** — they never touch your content or structure (see `99 System/_system/core-manifest.md`).

## v26.05.30-03 — 2026-05-30
- **Capture-style tasks surface on their object.** A task jotted anywhere (e.g. today's daily note) with a `[[link]]` to a project or person now appears on that object — added an "⤵ Captured elsewhere" Dataview query to the **project** and **person** templates, plus a convention and a `capture-triage` rule. Tasks stay inline `- [ ]` lines; the link does the surfacing.
- **Property setup is now recoverable.** `vault-health` reconciles `.obsidian/types.json` + `PROPERTIES.md` against `object-types.md` — registering/populating anything missing — so a skipped onboarding property-setup can be fixed anytime (run vault-health, or just ask).

## v26.05.30-02 — 2026-05-30
First round of trial-feedback fixes and polish.
- **Onboarding now reliably sets up properties** — it explicitly registers property types in `.obsidian/types.json` and populates `PROPERTIES.md` with controlled values (these were being skipped).
- **Link/list properties registered** (`area`, `with`, `org`) so wikilink properties render as links and don't break YAML.
- **Templates** — cleaner formatting; new **property order** (status first → `type` second-last → `created` last); added **Dataview relation queries** to `person`, `project`, and `event` (`area` already had them).
- **New convention:** property ordering (most-glanceable first).
- **AI Team Board** is Kanban-plugin compatible, with a tip to enable it.
- **Object-model canvas** — onboarding now builds/personalizes it explicitly; added a **user-first note** on the legend (editing the canvas doesn't auto-rewire your links).
- **obsidian CLI** hard rule reworded to "always use by default."
- **Principle #1** expanded into the explicit **user-first** design principle.

## v26.05.30-01 — 2026-05-30
Initial public release. A local-first, self-personalizing Markdown personal OS / second brain, maintained by an AI assistant: ships empty, an onboarding interview builds the structure around the user. Bring your own AI CLI; MIT-licensed.
