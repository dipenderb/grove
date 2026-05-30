# Relations Registry

The **dictionary** of how objects connect: each relation's meaning, direction, and wikilink syntax. Relations are `[[wikilinks]]` — in frontmatter (queryable) or inline in the body. This registry keeps the relation *names* consistent so the graph stays legible. Onboarding personalizes this list; new relations are added only when an existing one won't do.

> **The type-level map is canonical in `object-model.canvas`.** That Obsidian Canvas is the single source of truth for *which type relates to which type* (the graph). This file is the companion **dictionary** — what each relation means and how to write it. Keep them in sync: a new relation here should appear as a labelled edge there.

## Default relations

| Relation | From → To | How it's written | Meaning |
|----------|-----------|------------------|---------|
| `area` | any → area | frontmatter `area: "[[Health]]"` | the object's home domain |
| `with` | event → person | frontmatter `with: ["[[…]]"]` | participants in an event |
| `assigned_to` | task → person | inline/frontmatter `[[…]]` | who owns a task |
| `org` / `works_at` | person → note | frontmatter `org:` or body link | where a person works (an org is a `note` by default, or a custom `company` type if you track many) |
| `partner` | person → person | frontmatter `partner: "[[…]]"` | spouse / partner |
| `manager` / `reports_to` | person → person | frontmatter | reporting line |
| `about` | note/resource → any | body `[[…]]` | what a note concerns |
| `blocked_by` | task/project → any | inline note | dependency |
| `originated_from` | any → event/capture/day | frontmatter `from:` | provenance — where it came from |
| `related` | any → any | body `[[…]]` | loose association |

## Rules
- **Type a relation by cardinality.** Holds **one** link → a `text` property (`area: "[[Health]]"`). Holds **many** → a `multitext`/List (`with: ["[[…]]"]`). Register multi-value relations as `multitext` in `.obsidian/types.json` (single ones default to `text`, no registration needed). **Relation properties are never listed in `PROPERTIES.md`** — their options are the live notes, not a fixed value set.
- **Prefer an existing relation** before inventing one (mirrors the no-new-type discipline).
- **Always quote wikilinks in frontmatter:** `area: "[[Career]]"`. Lists use YAML list syntax.
- **Link, don't duplicate.** The relation *is* the connection; don't also copy the linked object's content.
- Backlinks are free: linking a person to an event makes that event appear on the person's note automatically. Lean on this instead of maintaining manual lists.

## Custom relations
_(empty — onboarding and ongoing use add the user's own, e.g. `client_of`, `advisor_to`, `treats` for a doctor→condition)_
