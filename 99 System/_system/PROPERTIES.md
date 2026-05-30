---
type: os-properties
updated: 2026-05-29
---
# Controlled Property Values

The canonical **allowed-value sets** for controlled-vocabulary properties — those whose value comes from a small, **fixed set of literals**. Three registries divide the work, no overlap:
- `object-types.md` — *which* properties each type has.
- `.obsidian/types.json` — each property's **type** (text / multitext / date…).
- **this file** — each controlled property's **allowed values**.

## How this becomes a "dropdown"
Obsidian core has **no enforced enum and does not read this file** — its property suggestions come from values already used in the vault. The dropdown effect comes from **discipline**: the assistant writes *only* values from the lists below, so the values in use stay exactly this set and Obsidian suggests precisely these. (A hard-enforced dropdown needs a community plugin; this file is the model-agnostic source of truth regardless.)

## Scope — list a property here only if its values are
- a **fixed set of literals** (e.g. `active`, `done`), **and**
- **not wikilinks** to other notes. A property whose values are `[[links]]` (`area`, `with`, `related`) is **not** listed here — its "options" are the notes themselves, not a fixed list.

Also excluded: unique free text (`full_name`, `email`, `url`), dates, numbers.

## Registry
| Property | Select | Allowed values |
|----------|--------|----------------|
| `project_status` | single | `idea` · `active` · `on-hold` · `done` · `dropped` |
| `area_status` | single | `active` · `dormant` |

*(Onboarding and `new-object-type` add rows for the kept/custom controlled properties — e.g. a `priority`: `low · med · high`, or a `goal_status`. Pair each with its type in `.obsidian/types.json`.)*

## Rules
- **One source of truth for values.** To add/rename/remove an allowed value, edit it **here first**, then fix affected notes. Never write a value that isn't listed here.
- **Type pairing:** a **single-select** controlled property is `text` in `types.json` (Obsidian autocompletes from the set); a **multi-select** one is `multitext` (List). Register the type by editing `types.json` directly — **never `property:set type=`** (see `properties-and-tags.md`).
- Keep each set small and human-readable. Prune unused values in `vault-health`.
