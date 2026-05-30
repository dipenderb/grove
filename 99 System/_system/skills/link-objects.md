# Skill: Link Objects

**Trigger:** Any time you create or edit an object, and during triage. Connecting is not a separate step — it's part of every write.
**Goal:** Keep the graph dense and correct. An unlinked object is nearly worthless; a well-linked one surfaces everywhere it's relevant for free.

## Rules
1. **Use the registry.** Connect with relations from `99 System/_system/relations.md`. Reuse an existing relation before inventing one; if you must add one, record it there.
2. **Every object gets three links minimum, where they exist:**
   - its **Area** (`area:`),
   - the **people** involved (`with:`, `org:`, etc.),
   - its **source** (`from: "[[2026-05-29]]"` — the capture or day it originated).
3. **Quote wikilinks in frontmatter.** Link the canonical file, never a copy of its text.
4. **Resolve or stub.** If a linked object doesn't exist yet, create a stub and link it (an unresolved `[[link]]` is a valid to-do for later).
5. **Lean on backlinks.** Don't maintain manual "related items" lists when Obsidian's backlinks already show every object that points here. Link once, see it everywhere.

## During triage
After classifying a capture into objects, before you finish: link them to each other, to their Areas, to the people, and back to the source day. Then they show up correctly in every relevant View.
