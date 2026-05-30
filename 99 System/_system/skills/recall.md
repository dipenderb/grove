# Skill: Recall

**Invoke:** `/recall`
**Trigger:** The user asks a question about their own life/data — "what do I know about X", "when did I last…", "what's open with…", "summarise my history with Y", "what's due this week" — **or about the agent's own activity** — "what did you do", "what changed in my vault", "when did you last touch X", "what have you been working on".
**Goal:** Answer from the graph — fast, accurate, token-efficient — and never fabricate.

**Two sources, pick by the question:**
- **About the user's life/data →** the **graph** (objects + backlinks), per the method below.
- **About what *the agent* did →** the agent's own **daily operational logs** (`99 System/_agent/logs/YYYY-MM-DD.md`) plus the `@AI Team Board.md` for in-flight work. This is why those logs exist: so the agent always knows what it executed on the vault and can recall it on demand.

Capture is only half the OS; this is the other half. The system earns its keep when the user can *ask it anything they've ever filed.*

## Method (frontmatter-first, minimal reads)
1. **Parse the question** into entities (people/companies), Area, type, and time window.
2. **Search frontmatter first.** Filter by `type`, `area`, dates, and links *before* opening any body — use the `obsidian` CLI search / Dataview when available, plain search otherwise. Open a note's body only when its frontmatter says it's relevant. This keeps reads (and tokens) low.
3. **Lean on backlinks.** A person's note already aggregates every event, project, and note linking to them — read those links, don't re-scan the vault.
4. **Synthesise a direct answer** in normal chat voice (this is *to* the user, not written into the vault — so the first-person voice rule doesn't apply here).
5. **Cite sources** as `[[links]]` so the user can click through.

## Rules
- **Never invent.** If it's not in the graph, say so plainly — then offer to capture it now.
- **Read minimally.** Prefer queries and frontmatter scans over full-text reads; this skill should be cheap to run.
- **Offer to persist.** If the answer reveals something worth keeping (a new fact, a follow-up), offer to create/update the object — don't silently write.
