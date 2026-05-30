# Object Type Registry

The canonical list of object types **in this user's OS**. Starts as the Core set; the onboarding interview personalizes it. This is the ledger — when a new type earns its place (per the 4-criteria audit in `architecture.md`), it gets a row here and a template **generated into `99 System/Templates/<type>.md`** (the reference patterns live in `99 System/_system/template-library/`; `Templates/` holds only kept types).

> Status: **DEFAULT (not yet personalized)** — replace this line with `PERSONALIZED — YYYY-MM-DD` after onboarding.

**Companion registries:** how objects *connect* lives in `relations.md`; how properties & tags are kept minimal and non-duplicative lives in `properties-and-tags.md`; how raw input *maps to* these types lives in `skills/classify-object-type.md` and its learned rules in `classification-learnings.md`. The property columns in the table below *are* the property registry — keep them eyeball-able.

---

## Active types

These are the **near-universal defaults** — proposed at onboarding as a starting set, kept/dropped/renamed by the user, never imposed. The vault ships with none of them instantiated; onboarding (or a "skip") creates the ones the user keeps.

The **title is the filename** — no `title` field (see `conventions.md`). Templates are generated to `99 System/Templates/<type>.md` for kept types, from `_system/template-library/`.

| Type | Purpose | Required fields | Key optional fields |
|------|---------|-----------------|---------------------|
| `area` | Life domain / Space — its note is the area's **dashboard/index** (live queries of everything linked to it) | `type, created` | `area_status` |
| `person` | A human | `type, created` | `full_name, area, role, org, email, phone, relationship` |
| `project` | Time-bound effort | `type, created, area` | `project_status, due, outcome` |
| `event` | Dated happening | `type, created, date` | `area, with, location` |
| `note` | Reference / thought | `type, created` | `area, tags` |
| `resource` | File / link / reference | `type, created` | `area, url, source` |
| `daily` | A day's journal note | *none — **identified by the Journal folder**, not a `type` field; date parsed from the filename* | `#ai-processed` (added when processed) |
| `weekly` | A week's review note | *none — **identified by `Journal/Weekly/`**; week from the filename* | — |

`person.full_name` holds the **formal name** (e.g. `Priya Nair`) when the filename is the everyday name you call them (e.g. `Priya`). Omit it when the filename already is the full name.

## Recognition signals — how raw input maps to a type

**The single source for classification.** When the user dumps anything, the `classify-object-type` skill matches it against these signals to identify which object(s) it contains — then creates, links, and files them. **Every type, default or custom, must have a row here** so it can be recognised later; a type with no signature is invisible to auto-filing. Each signal also notes how to disambiguate from look-alike types.

| Type | Recognise by | Not to be confused with |
|------|--------------|--------------------------|
| `person` | A human name; contact info (email/phone); a role/title; "met / spoke with / intro'd to" | A company (org name, not a person) |
| (an org / company) | An organisation name; "the firm / bank / fund / vendor"; a website | Record as a `note` by default (or add a custom `company` type if you track many orgs); a person who works there → `person` |
| `event` | A specific date/time **+** people **+** often a place; "meeting / call / lunch / appointment" | A future intention with no date → `task`; a multi-step effort → `project` |
| `project` | A multi-step effort with an outcome and a rough deadline; "launch / build / plan / organise / renovate" | A single action → `task` (a line); an ongoing domain → `area` |
| `task` (a line, not a file) | A single actionable verb doable in one sitting; optional due date | Multi-step w/ outcome → `project` |
| `note` | A durable fact, idea, or insight; **no** action, **no** date | A saved link/file → `resource` |
| `resource` | A URL, a file, "read / watch / save / reference this" | A free-form thought → `note` |

> **Custom / optional types** added at onboarding or via `new-object-type` get their own rows here — same two columns. Examples: `goal` — *recognise by:* an aspirational outcome + a horizon ("this year", "by Q3") + a measure; *not confused with:* a concrete effort toward it → `project`. Or `gig` (a musician) — *recognise by:* a performance date + a venue + a fee; *not confused with:* a generic `event`. (`goal` is **not** a shipped default — add it only if you track outcomes/OKRs.)

## Tasks (not a type)

Inline checkboxes in any note, in Tasks-plugin emoji syntax:
`- [ ] Call the bank 📅 2026-06-02 ⏫` (due 📅, scheduled ⏳, priority ⏫🔼🔽, done ✅).
This format is used **regardless of whether the Tasks plugin is installed** (`tasks_mode` in `config.md`) — it stays queryable via Dataview and lets the user enable the plugin later with no rewrite. Surfaced by the task smart-lists in `@Tasks/` (Today, Open, …) — built on request, separate from `@Dashboards/`. Promote to a `project` only when multi-step with a real outcome.

---

## Status & other controlled values

Each type's status is a **distinct, type-prefixed property** (different value sets — never a bare `status`). The **allowed values** for `project_status`, `area_status`, and every other controlled-vocabulary property live in `PROPERTIES.md` (the single source for legal values, and what keeps Obsidian's suggestions clean). Add or rename values there — not here.

---

## Change log

Record every type added/renamed/removed here, with date and the criteria that justified it.

| Date | Change | Justification |
|------|--------|---------------|
| (seed) | Core set created | Default scaffold |
