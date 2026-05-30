# Properties & Tags — Keep the Taxonomy Small

The single source of truth for frontmatter properties and tags. The biggest long-term risk to a markdown OS isn't too few features — it's metadata sprawl: dozens of fields and tags nobody remembers or maintains. These rules keep the set **small enough to manage by hand, with or without the AI.**

---

## One job each — don't overlap the tools

You have four ways to attach meaning. Each has exactly one job. Confusing them is what creates sprawl.

| Tool | Use it for | Never use it for |
|------|------------|------------------|
| **Link** `[[ ]]` | Connections between objects (person → company, task → project, anything → its Area) | Attributes or status of a single object |
| **Property** (frontmatter) | A handful of attributes of *this* object that a dashboard must filter or sort on (`project_status`, `due`, `area`) | Connections (use a link) · themes (use a tag) |
| **Tag** `#x` | Cross-cutting themes or states you filter *across many object types* (`#waiting`, `#someday`) | Anything a link or property already expresses |
| **Body prose** | Everything else — context, narrative, detail | Facts a View needs to query (those earn a property) |

---

## The golden rule: no duplication

**A fact lives in exactly one place.**

- If `area: "[[Health]]"` is set, do **not** also add `#health`. The link already says it.
- If a person links to their company, don't also store the company name as a text property.
- **Never store what can be derived.** Store a birthdate, not an age. Store a `due` date, not "overdue" — a query computes that.
- If you find yourself copying a value between files, stop — **link the source instead.**

---

## Adding a property — the gate

Add a property **only if a dashboard needs to filter or sort on it.** If you'd never query it, it's body prose, not a property.

Walk these, stop at the first that fits (mirrors the no-new-type gate):
1. Can a **link** carry it? → link, no property.
2. Can **body prose** hold it? → prose, no property.
3. Does a **View actually query it**? → only now, a property.

Naming:
- Short, **lowercase**; **underscores** for multi-word names (`full_name`), **never hyphens** — a hyphen breaks Dataview (`area-status` parses as *area minus status*).
- **Disambiguate before you collide.** Reuse a bare name across types **only when the meaning *and* the value set are identical everywhere it appears** (`area` link, `due` date, `created` — same concept everywhere). When the same concept carries a **different value vocabulary per type**, **prefix it with the type** so a cross-type query never silently mixes them: use `project_status` (idea/active/on-hold/done/dropped) and `area_status` (active/dormant) — **not a bare `status` on both** (a `WHERE status = "active"` would sweep up both projects and areas). Same value set → share the name; different value set → namespace it.
- **Reuse before inventing** otherwise: one concept, one name across types — `due` everywhere, not `deadline` here and `by` there.
- The canonical property list per type lives in `object-types.md`. That table *is* your registry — keep it eyeball-able.

---

## Property types — Text · List · Date (and how to register them)

Pick the Obsidian property type by the **shape of the value**:

| Type (in `types.json`) | Use when | Examples |
|------------------------|----------|----------|
| **`text`** | Value is **unique per note**; *or* a single value from a known set (Obsidian autocompletes `text` from used values, keeping `active`/`done` consistent without a list); *or* a **single relation** holding one `[[wikilink]]`. | `full_name`, `email`, `url`, single-value `*_status`, `area: "[[Health]]"` |
| **`multitext`** (List) | A **multi-value** field — either a controlled literal set you want suggested, **or a relation holding many `[[wikilinks]]`**. | `tags` (literals); `with`, `related` (links) |
| **`date`** / **`datetime`** | A calendar value. | `created`, `due`, `date` |
| **`number`** / **`checkbox`** | Numeric / boolean. | counts, flags |

**Relation (wikilink) properties** are typed purely by **cardinality** — one link → `text`, many → `multitext` — and are **never listed in `PROPERTIES.md`**, because their options are live notes, not a fixed value set. Only `multitext` *literal* sets (like a custom enum) get values in `PROPERTIES.md`; `multitext` *link* lists do not. (Relation dictionary: `relations.md`.)

**Registering a type — the critical gotcha.** Obsidian keeps a property's **type** in `.obsidian/types.json` (the registry) and its **value** in each note's frontmatter — *two separate concerns.*
- **To set/change a property's TYPE → edit `.obsidian/types.json` directly** (`"<prop>": "multitext"` for List, `"date"`, `"text"`…). It's an Obsidian-owned file, edited as a plain file.
- **To set/change a property's VALUE in a note → use the `obsidian` CLI.**
- **Never run `obsidian property:set type=…`** — it touches the note instead of the registry and **corrupts it** (injects a garbage `- ""` empty list item instead of a clean `[]`).

> One line: **type registration lives in `.obsidian/types.json`, not in the note.**

**Allowed values** for controlled-vocabulary properties (fixed literal sets — not wikilinks) live in **`PROPERTIES.md`**. The assistant writes only values listed there, which keeps Obsidian's value suggestions clean (a de-facto dropdown). Add a value there before using it.

---

## Adding a tag — the gate

Add a tag **only if** (a) you will filter across objects by it, **and** (b) no property or link already says it.

- **Flat, lowercase, kebab-case.** No hierarchies (`#work/clients/active`) — that's what Areas and links are for.
- **One concept, one tag.** Don't let `#health`, `#fitness`, `#wellness` coexist for the same idea — pick one and stick to it.
- Keep the **whole tag vocabulary small enough to fit on one screen.** If you can't list every tag from memory, you have too many.
- A tag that isn't in the registry below shouldn't exist. Add deliberately.

### Tag registry (the allow-list)
The complete set of tags in this OS. Cross-cutting *states* that span types — kept minimal on purpose. Onboarding and real use personalize this; prune in `vault-health`.

- `#waiting` — blocked on someone else
- `#someday` — not now, maybe later
- `#idea` — unformed, not yet a project
- `#follow-up` — needs a touch, no formal task yet
- `#ai-processed` — a daily note the agent has finished processing; the human's signal it's safe to file into the Journal year/month archive

_(Add to this list only when a new cross-cutting filter genuinely earns it.)_

---

## Maintaining it — a 5-minute job, by hand

This is designed to be maintainable **without the AI layer**:

- **Monthly**, skim the property tables in `object-types.md` and the tag registry above. Anything unused for ~2 months → remove it (demote a property to prose; delete a tag).
- `vault-health` automates this audit — but you can do it yourself in five minutes. That's the whole point of keeping the set tiny.
- **When in doubt, don't add.** It's cheap to add a property later when a real query needs it; expensive to un-sprawl a vault full of dead metadata.
