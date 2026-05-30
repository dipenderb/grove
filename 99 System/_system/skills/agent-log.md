# Skill: Agent Workspace Upkeep (board + log + memory)

**Trigger — active, not "session end".** Run this **in the same turn**, right after you act on the OS: created/edited/linked an object, took on or finished a work item, made a routing or classification decision, hired a teammate. A chat has no detectable "session end" — if you wait for one, nothing gets recorded. Act → update.
**Goal:** Keep the shared work queue and your own workspace a true, current record of what's happening — so the human can see and steer at any moment.

## 1. Keep the Board current (every time a work item changes state)
Update `/@AI Team Board.md` whenever you **take on, progress, finish, or accept** any work: move its line between **Queued → In-progress → Recently delivered**, note who's on it, and link the deliverable/object. This is not optional — a stale board breaks the human's ability to steer. (Trivial one-off chat answers that create nothing don't need a line; any real work does.)

## 2. Log it — your daily operational record (every time you act)
Maintain **one log file per day**, always — it's the record of **everything you executed on the vault**, so you can recall it on demand ("what did you do / change / touch X?" → you read these, per the `recall` skill).
1. Run `date`. Target `99 System/_agent/logs/YYYY-MM-DD.md` — create with frontmatter (`type: agent-log`, `date:`, `tags:`) if new, else **append**.
2. Add terse, timestamped bullets for each vault action: objects **created / edited / moved / archived / linked** (link them `[[…]]`), decisions made, jobs routed to a teammate, corrections learned (link to where the rule was recorded). Enough that future-you can reconstruct what changed and why. The log is your *private* history; the **Board** is the *shared* live state — keep both, don't conflate.

## 3. Remember durable facts (only on genuine learning)
Write or update `99 System/_agent/memory/<kebab-topic>.md` when you learn something that will change how you **operate in future sessions**: a recurring user workflow, where something lives, a preference in how you should work, a failure pattern to avoid. **Not every turn** — only real, durable operational learning. Check for an existing topic file first and update it; don't duplicate.
- **Not here:** vault-content learnings — classification → `../classification-learnings.md`, voice → `../writing-style.md`. Link, never copy. Memory is about *me operating*, never a cache of the user's content (read that live).

## Rules
- **First person as the agent** ("Triaged 5 captures, created 2 people…"), never as the user.
- **Token-efficient:** bullets and links, not narration. Don't restate what lives in the objects — link.
- **Atomic & append-only:** one log file per day; one memory file per topic; never rewrite history.
- **Separation:** these files live **only** in `99 System/_agent/`. Plain `-` bullets, never `- [ ]` — so your work never leaks into the human's task views.
