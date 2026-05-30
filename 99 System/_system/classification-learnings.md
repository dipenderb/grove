# Classification Learnings

Append-only. Records two kinds of personalization, consulted **before** the default signal tables in `skills/classify-object-type.md`:
1. **Corrections** — every time the user re-files or re-types something, capture the rule so it isn't repeated.
2. **Standing routing/handling rules** — deliberate choices about how a kind of input is handled, including from onboarding. Notably: when a type was *declined*, how that information lives instead (e.g. touchpoints logged in the daily note with links rather than as `event` objects).

Format:
`- <signal / pattern> → <type or destination> (learned YYYY-MM-DD; was: <wrong thing, if a correction>)`

## Learned rules
_(empty — fills from onboarding choices and the user's corrections. Example: `- a meeting/call/touchpoint → append to today's daily note + link participants; do NOT create an event object (set at onboarding 2026-…)`)_

## Promotion candidates
Rules that have held repeatedly and could become defaults in the signal table. `vault-health` reviews these.
_(empty)_
