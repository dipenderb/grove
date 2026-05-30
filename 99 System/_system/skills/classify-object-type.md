# Skill: Classify Object Type

**Trigger:** Used inside capture-triage (and whenever you must decide "what is this?"). The classification engine of the OS.
**Goal:** Map raw input → the right typed object(s), reliably, and get *better at it over time*.

---

## Step 0 — Load the two sources, in order

1. **Recognition signals** in `99 System/_system/object-types.md` — the single registry of how each type (default **and** the user's custom types) is recognised, with disambiguation notes. This is what lets a type built at onboarding be identified later.
2. **Learned corrections** in `99 System/_system/classification-learnings.md` — these **override** the registry signals. A rule the user taught once ("receipts → resource, not note") wins every time after.

Classify against *this user's* type set, never just the Core defaults.

---

## Step 1 — Match signals → identify every object present

Match the input against the **Recognition signals** registry (loaded in Step 0). One dump often contains **several** objects — decompose it fully (an email → a `person` + an `event` + an inline task). Don't stop at the first match; scan for every type present.

If the input matches no signature and no escape hatch fits, leave it as a **capture** and ask in one line — or, if it's genuinely a new kind of thing, run `new-object-type.md` (which adds a recognition signature so it's caught next time).

## Step 2 — Decision procedure

1. **People first.** For every person named, link the existing `20 People/` object or create a stub. People anchor the graph.
2. **Dated happening?** → `event`, linked to its people, Area, and source day.
3. **Action present?** → an inline `- [ ]` task on the most relevant object. Only spawn a `project` if it's multi-step *with an outcome* (escape hatch: a task is a line, not a type).
4. **Durable knowledge?** → `note` or `resource`.
5. **Assign an Area** to each object. If unclear, infer from the people/projects it links to; if still unclear, ask.
6. **Apply minimalism** (`architecture.md`): if it fits no type, run `new-object-type.md` — don't invent a type casually.

## Step 3 — The learning loop (how it gets smarter)

The system learns from **corrections**, not from being told it's right.

- **When the user re-files, re-types, or renames** something you classified, treat it as training. Append a rule to `99 System/_system/classification-learnings.md`:
  `- <signal> → <type> (learned YYYY-MM-DD; was misclassified as <wrong type>)`
- **Before next classification**, those rules are consulted in Step 0 and override defaults.
- **Promotion:** when a learned rule has clearly held over many captures, `vault-health` proposes folding it into this skill's signal table (or the type registry) so it becomes a first-class default.

Goal: **misclassify the same thing at most once.**

## Step 4 — Confidence & ambiguity
- High confidence → classify and proceed; report what you did.
- Low confidence → make the obvious calls, then ask one tight question for the rest. Never guess the user's *intent* on something consequential.
