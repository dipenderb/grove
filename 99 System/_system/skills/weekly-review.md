# Skill: Weekly Review

**Invoke:** `/week`
**Trigger:** Start of a week, or user asks to "review my week."
**Goal:** Step back from objects to patterns — close loops, surface what's drifting, set the week ahead.

## Steps
1. Run `date`. Determine ISO week (`YYYY-Www`). Target: the Journal's `Weekly/YYYY-Www.md` (resolve the Journal folder from Obsidian — don't hardcode a number).
2. Gather the week's signal:
   - Daily notes from the past 7 days (in the Journal folder — root or the current `YYYY-MM mmm/` month folder).
   - Projects: what moved, what stalled (`project_status`, last-modified).
   - Tasks: completed this week, overdue, slipping.
   - New people / events / captures triaged.
   - *(If a `goal` type exists)* goals: progress vs. horizon.
3. Write the review (template below). Be honest and specific — name what's drifting, don't just list.
4. **Act on it:** archive done projects, roll forward or drop stale tasks, flag any Area that got no attention, and propose 3 priorities for the coming week. (Deeper drift/sprawl/orphan sweeps are `vault-health`'s monthly job — here, just close *this week's* loops.)
5. Surface to the user in 5–6 lines: wins, drifts, decisions needed, next-week focus.

## Template
```markdown
## Wins
## Moved
## Stalled / drifting
## People & touchpoints
## Goals — progress
## Next week — top 3
```
**No frontmatter** — like dailies, weekly notes are identified by their folder (`Journal/Weekly/`); the week comes from the filename (`YYYY-Www`).

Cadence note: this is where the OS earns its keep. Object-level capture is daily; pattern-level synthesis is weekly. Don't skip it.
