# Skill: New Object Type

**Trigger:** A capture genuinely doesn't fit any existing type, or the user asks to track a new kind of thing.
**Goal:** Add a type **only when it earns its place** — and keep the registry honest.

This skill is mostly a gate. Most of the time, the answer is *don't create the type.*

## Gate (from `architecture.md`)

Walk the three escape hatches **in order. Stop at the first that works.**
1. **Field** on an existing type? → add a frontmatter field, done.
2. **Relation** to another object? → wikilink, done.
3. **Inferable** from linked objects? → nothing to add, done.

Only if all three fail, run the **4-criteria audit**. The type ships only if it satisfies **≥ 2 of 4**: distinct relationships · distinct lifecycle · distinct origin · distinct reasoning.

**Smell test:** "Is explaining this as *'a kind of [existing type] that…'* more confusing than adding a field?" If no → stop.

## Onboard the type (a mini-interview)
Adding a type means **getting onboarded to it** — the system can't recognise, classify, or connect something it doesn't understand. Before creating anything, ask the user (one line each, reflect back):
- **Context:** what is this in your world, and what does one note represent? (singular type name; one note = one instance)
- **Identify/classify:** how would I spot it in a raw dump — what signals give it away, and what's it *not* to be confused with?
- **Relate:** which existing types does it link to, and how? (the relation vocabulary)

This is the same per-type discovery onboarding does — just for one new type. Keep it quick; it sharpens with use.

## If it passes — record what you learned
1. Add a row to `99 System/_system/object-types.md` (singular type name, purpose, required/optional fields — no `title` field; the filename is the title).
2. **Recognition signature** → the *Recognition signals* table in `99 System/_system/object-types.md` (from "identify/classify" above). Without it, the type can't be auto-identified from a dump.
3. **Canvas** → add a node to `99 System/_system/object-model.canvas` plus a labelled edge for each relation (from "relate" above). Update `relations.md` if a new relation was introduced.
4. **Template** → generate `99 System/Templates/<type>.md` with the minimal field set (no `title` field) — resist field sprawl as hard as type sprawl. For a near-universal type, also drop a copy in `99 System/_system/template-library/` so it's reusable. **Register any new property's type** in `.obsidian/types.json` (dates → `date`, controlled multi-value sets → `multitext`); **never `property:set type=`** (see `properties-and-tags.md`). If the new type has a **controlled-vocabulary** property, add its allowed values to `PROPERTIES.md`.
5. **Home folder** → create it as the **plural** of the type (`gig` → `Gigs/`) with a one-line `_README`, unless it sensibly shares an existing folder.
6. If a dashboard would help, add a View in `@Dashboards/`.
7. Log the change in the registry's change log — date + which criteria it met.

Report to the user: the new type, why it cleared the gate, and where to create instances.
