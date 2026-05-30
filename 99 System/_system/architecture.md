# Architecture — The Object Model

The single source of truth for how this OS is structured. Adapted from a company-OS architecture into a single-user, local-first, markdown system. Read this before making any structural decision.

---

## Five principles

1. **Universal object model.** Everything is an object: a markdown file with frontmatter carrying a `type`. A new kind of thing is a new `type` value — never a schema migration, never a new app. People, projects, notes, events, goals — same primitive, different `type`.

2. **Areas are Spaces.** Every object belongs to one life domain (Area). Areas give objects a home and scope the dashboards. **An Area's note is its dashboard/index** — open it and see everything linked to that area (goals, open tasks, active projects, upcoming events, people, recent notes) via live queries on the `area` field. (A company OS uses Spaces for access control; a single-user OS uses Areas purely for organization and focus.)

3. **Relations over fields, fields over types.** Connections between objects are `[[wikilinks]]`, not duplicated text. The link graph carries meaning. Prefer linking to two objects over inventing a third type to join them.

4. **Capture → enrich → file → surface.** Unstructured input never goes straight to its final home. It lands in `00 Inbox/`, gets enriched into typed objects, gets linked, and shows up in a View. The pipeline is the same regardless of source.

5. **Minimalism is the whole game.** A universal object model rots the instant you let types and fields multiply (the "Salesforce trap"). Restraint is what keeps it legible for years. Default to *no new type*.

---

## What an object is

A markdown file:

```markdown
---
type: person          # the discriminator — what kind of object this is
area: "[[Health]]"    # which Space/Area it belongs to (wikilink)
created: 2026-05-29
tags: [doctor]
# …type-specific fields…
---

Free-form markdown body. Notes, context, history.
Relations to other objects as [[wikilinks]] inline or in frontmatter.
```

- **`type`** and **`created`** are required on every object.
- **`area`** is expected on most objects (the Inbox and system files are exceptions).
- Everything else is type-specific and lives in frontmatter (for querying) or the body (for prose).

---

## The minimalism discipline — before you create a new type

Most things that *feel* like a new type are a variant of an existing one. Walk these **three escape hatches in order. Stop at the first that works.**

1. **A field on an existing type?** Can a frontmatter field capture the variation? (A `status`, a `category`, a date.) → field, no new type.
2. **A relation to another object?** Is this really "X relates to Y"? (A "gym membership" is a `[[Project]]` or `[[Resource]]` linked to `[[Health]]`, not a Membership type.) → wikilink, no new type.
3. **Inferable from context?** Can you tell what this is from the objects it links to? → no field, no type.

Only if **all three fail**, run the 4-criteria audit. A new type must satisfy **at least 2 of 4**:

| # | Criterion | Test |
|---|-----------|------|
| 1 | Distinct relationships | Connects to other objects with fundamentally different semantics |
| 2 | Distinct lifecycle | Has its own state progression that isn't just a `status` flag |
| 3 | Distinct origin | Created through a fundamentally different pathway |
| 4 | Distinct reasoning | You must think about it categorically differently to act on it |

**Smell test:** "Would explaining this as *'a kind of [existing type] that…'* be more confusing than just adding a field?" If no → don't make the type.

---

## Field discipline (when a field IS the answer)

Even fields sprawl. Order of preference:

1. **Relation (`[[wikilink]]`)** — anything that points at another object.
2. **Frontmatter field** — type-specific properties you'll filter or sort on (status, due, value).
3. **Body prose** — everything else. Context, narrative, detail. Don't promote prose to a field unless a View needs to query it.

The practical discipline for *growing and maintaining* properties and tags — the no-duplication rule, the add-a-property / add-a-tag gates, the tag allow-list, and the by-hand maintenance routine — lives in `99 System/_system/properties-and-tags.md`.

---

## Default object types (Core set)

The starting registry. The onboarding interview adds, renames, or removes types to fit the user. The canonical, personalized list lives in `99 System/_system/object-types.md`.

Folder = the **plural** of the type, **numbered by frequency** at onboarding (most-used on top, e.g. `10 Projects/`). The names below omit numbers since onboarding assigns them per user.

| Type | What it is | Lives in |
|------|------------|----------|
| `area` | A life domain (Space). The container. | `Areas/` |
| `person` | Anyone — family, friend, colleague, contact, professional. | `People/` |
| `project` | A time-bound effort with an outcome. Linked to an Area. | `Projects/` |
| `note` | A piece of reference knowledge or a thought. | `Notes/` |
| `event` | A meeting, appointment, trip, or dated happening. | Area or `Journal/` |
| `resource` | A file, link, or external reference. | `Resources/` |
| `daily` / `weekly` | Journal entries. | `Journal/` |

(`goal` is an optional add-on, not a default — add it via `new-object-type` if you track outcomes/OKRs.)

**Tasks are not files by default.** A task is an inline checkbox in any note (`- [ ] thing 📅 2026-06-01`), surfaced by query. Promote a task to a `project` only when it has multiple steps and an outcome worth tracking. (Escape hatch #1 in action: a task is a *line*, not a *type*.)

---

## Relations — the connective tissue

Express every connection as a wikilink. Common relation patterns:

- Person → Area: a contact's domain. `area: "[[Health]]"`
- Person ↔ Person: `partner: "[[…]]"`, `manager: "[[…]]"`
- Project → Area: `area: "[[Career]]"`
- Object → Person: `with: "[[Priya Nair]]"` on an event
- Anything → source: `from: "[[2026-05-29]]"` (the capture/day it originated)

The graph is the value. A person's note accumulates every event, project, and note that links to them — Obsidian's backlinks surface this for free.

**The type-level relationship map is `99 System/_system/object-model.canvas`** — an Obsidian Canvas where nodes are object *types* and labelled edges are the relations between them. It is the canonical, at-a-glance source of truth for how types connect; `relations.md` is its companion dictionary (per-relation meaning and syntax). Both are kept in sync as types and relations evolve.

---

## Views — presentation is decoupled from data

Object types describe **what exists**. Views describe **how to see it**. They are independent: a new View touches no object; a new object type just appears in compatible Views.

In Obsidian, a View is a note in `@Dashboards/` containing a **Dataview** (or Bases) query. Examples: "all open tasks due this week," "every person in Health," "active projects by Area." The query reads the object graph; it never owns it.

Adding a calendar view, a kanban, a table — all the same data, queried differently. Don't fork your data to get a new view; write a new query.

---

## Capture pipeline

```
Raw input ─▶ 00 Inbox/ ─▶ enrich ─▶ typed object(s) ─▶ link ─▶ surface in View
 (thought,    (capture     (extract   (person, event,   (wiki-   (dashboard)
  email,       object)      people,    project, note)    links)
  voice,                    dates,
  photo)                    actions)
```

Every capture is preserved until explicitly triaged. Triage relocates and structures; it never silently deletes. See `99 System/_system/skills/capture-triage.md`.

---

## What this OS is *not*

- **Not a task manager replacement** — it coordinates above your tools, it doesn't compete with a dedicated to-do app's UX. Tasks are lightweight lines here.
- **Not a document editor / wiki** — structured operational data, not long-form docs. Long docs stay in dedicated tools and get linked as `resource` objects.
- **Not a chat app** — no threads. You communicate with the OS by creating and editing objects.
- **Not cloud-dependent** — it works fully offline. Sync (Drive, iCloud, git) is transport, never the source of truth.
