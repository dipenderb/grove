# Skill: Process Daily Note

**Invoke:** `/process-today`
**Trigger:** `capture_layer` is `daily-note` (see `config.md`) — or the user asks to process daily notes.
**Goal:** Turn a free-form daily log — which may hold ~10 unrelated notes across many lines — into structured, linked objects, losing nothing.

**Scope = every daily note WITHOUT the `#ai-processed` tag.** The tag is the processing filter: an untagged daily note is unprocessed, a tagged one is done. So this runs over today's note *and any backlog* of untagged dailies (in the Journal folder root, plus any the human hasn't archived yet). Process each, then tag it.

This is the **orchestrator** skill for daily-note capture: it segments the log, detects each block's content type, and **invokes the right content-skill** for it. It does the routing; the child skills do the processing (atomic, modular, interlinked).

## 1. Find unprocessed dailies, read each
Resolve the daily-note folder + date format from Obsidian (`.obsidian/daily-notes.json`, or `obsidian daily:read`) — don't assume a literal path. **Identify daily notes by location — notes inside the Journal folder** (the resolved daily-note root plus its `YYYY-MM mmm/` month folders; archived years live in `Archive/Journal/YYYY/`), not by a property or by parsing filenames. Among those, list the ones **lacking `#ai-processed`** (today's + any backlog); process each in turn. When you need a note's date, parse its filename using the `format` from config (or use Dataview's `file.day`). Read the log/capture section of the one you're on.

## 2. Segment into blocks (group with context)
A day's note can contain many unrelated notes, each possibly spanning several lines. **Group lines into coherent blocks — one block = one thought/topic.** Use blank lines, bullets, headings, and topic shifts as boundaries; keep multi-line notes about the same thing together so context isn't lost. When a boundary is ambiguous, prefer keeping related lines together; ask only if it really matters.

## 3. Detect each block's content type & route
For each block, detect what it is and **invoke the matching content-skill**:
- **Article link** → `process-article`
- **YouTube / video link** → `process-yt-video`
- **Audio / voice note** → `process-audio`
- **Image / screenshot** → `process-screenshot`
- **Plain text** → handle inline via the text logic (step 4)

Each content-skill does its own (delegated) fetch/transcription/OCR and files the result. You only route — one block → one skill. A block with several parts (a line of text *and* a link) routes each part to its skill.

## 4. Text: object-or-mentions (the key decision)
For a text block, decide which of two cases it is — see the same logic in `capture-triage.md`:
- **The whole block IS one object** — "Renovate the kitchen — get 3 quotes" (`project`); "Coffee with Priya re funding" (an interaction/event, or a linked log entry per the user's handling rule). → classify its type (recognition signatures), create the object, set its relations, link the log line to it.
- **The block is NOT itself an object, but mentions some** — "Priya thinks ICICI will move fast on the export deal." → don't make the sentence an object; **find the objects named inside it** (Priya → person, ICICI → company, the deal → project) and **wikilink those in place**, leaving the sentence as a linked log entry.

Use `classify-object-type` for types and `link-objects` to connect. Respect recorded handling rules (touchpoints may stay as linked log entries rather than objects).

## 5. Link, preserve, tag `#ai-processed` — and leave it for the human to file
Link everything to its people / areas / projects and to the day. **Never destroy the original log** — leave it intact (the structured objects become the queryable record). When the note is fully processed, **add `#ai-processed` to its frontmatter `tags`** and **leave it exactly where the Daily Notes plugin created it** (the Journal folder root). Do **not** move or reorganise it — the human files processed dailies into the active month folder (`Journal/YYYY-MM mmm/`) themselves; the tag is their signal that it's safe to move. Summarise to the user: what was created, what was linked, and anything ambiguous.
