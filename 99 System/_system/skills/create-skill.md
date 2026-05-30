# Skill: Create Skill

**Invoke:** `/skill` (or just describe a routine and the assistant proposes it)
**Trigger:** You notice **repeatable work** — the user asks for the same kind of thing more than once, or describes a routine ("every morning I want…", "always do X when Y") — or the user explicitly says "make this a skill."
**Goal:** Codify the repeatable procedure as a new, atomic, **invocable** skill, and tell the user how to call it.

This is the OS growing its own procedures — the same restraint as new object types and new teammates applies: build a skill only for genuinely recurring work.

## 1. Spot it (always watching)
Stay alert for repeatability and **propose** when you see it — don't build silently:
*"You've asked for your day plan a few mornings now — want me to make it a one-tap routine? You'd just type `/today`."* Confirm before building.

## 2. Clarify (if needed)
Ask what the routine should do and the user's preferences — what to include, the order, filters, when it runs. Reflect back in one line. Keep it quick.

## 3. Build it — adhere to the design principles
1. **Atomicity** — one skill = one procedure, one job. Write it to `99 System/_system/skills/<name>.md`.
2. **Modularity + interlinking** — **reuse, don't duplicate.** Reference existing skills instead of re-describing their steps. (e.g. a `/today` skill *calls* `daily-note` + `recall` rather than restating them.)
3. **Invocation** — give it a short `/name` the user types (`/today`, `/week`). Put `**Invoke:** /name` near the top of the skill, and add a row to the skills table in `AGENTS.md` (Skill · Invoke · Trigger · File).
4. **Model-agnostic** — the invocation is a shortcut the assistant recognises in any CLI; where native slash-commands exist it can also be realised there, but the skill file is the source of truth.

## 4. Tell the user how to use it
State it plainly: *"Done — type `/today` any morning and I'll give you your day plan."* Always close the loop so the new skill is actually used.

## 5. Keep the skill set clean
Don't multiply near-duplicate skills — extend an existing one instead. `vault-health` prunes skills that stopped being used.
