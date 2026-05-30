# Skill: Capture Triage

**Trigger:** New captures present in the capture layer, or the user drops something to capture.
**Goal:** Turn raw input into structured, linked objects — without ever losing the original.

The **capture layer** is set by `capture_layer` in `99 System/_system/config.md` — check it first:
- `inbox` (default): captures are files in `00 Inbox/`.
- `daily-note`: captures are appended lines in today's note. **Resolve the daily-note folder/format from Obsidian (`.obsidian/daily-notes.json`) or use `obsidian daily:append`** — don't assume the literal `40 Journal/Daily/YYYY-MM-DD.md`.
External channels (email-forward, etc.) always land in `00 Inbox/` regardless.

---

## Capturing (input → capture layer)

When the user hands you anything (a thought, forwarded email, voice transcript, photo of a card, a link):

- **If `capture_layer: inbox`** — run `date`, create `00 Inbox/YYYY-MM-DD HHMM <short-slug>.md`: a `capture` note with frontmatter `type: capture`, `created:`, `source:` (manual/email/voice/image/link), raw content verbatim in the body.
- **If `capture_layer: daily-note`** — append the raw line to today's daily note under a Log/Capture section (run `date` for the filename); the day's note *is* the capture record.

Don't enrich yet if the user is mid-flow — just preserve it. Enrich on triage.

## Triaging (Inbox → typed objects)

**Autonomous by default — your job is to offload the user.** When something is dumped, identify *every* object it contains (via `classify-object-type`, which reads the recognition signatures for their custom types), create each one, link and connect them, and file them — then report. Ask the user only when there's a genuine decision you can't make, not for routine filing. The user dumps; the system handles it.

For each capture, work top to bottom:

1. **Read and classify.** What is this really? An interaction with a person? A task? A new project? Reference material? A date to remember?
2. **Extract entities.** Pull out people, companies, dates, amounts, actions. Resolve relative dates to absolute (`date` first).
3. **Match or create.** For each person/thing mentioned, link to the existing object if one exists (`20 People/…`); if not, create a stub and link it.
4. **Produce the typed object(s).** Apply the right template. One capture can spawn several objects (an email → one `event` + one new `person` + one inline task).
5. **Link everything.** Wikilink the new objects to each other, to their Area, and back to the source day. Add a task as an inline `- [ ]` where an action exists.
6. **Resolve the capture.** Move the original to `99 System/Archive/Inbox/` (don't delete) or, if fully absorbed and trivial, note it as processed. The structured objects are now the record.

## Content types — route by what it is
A capture (or a daily-note block) can be more than plain text. Detect the type and **invoke the matching content-skill** (same set `process-daily-note` uses):
- **Article link** → `process-article`
- **YouTube / video link** → `process-yt-video`
- **Audio / voice note** → `process-audio`
- **Image / screenshot** → `process-screenshot`
- **PDF / file** → a `file`/`resource` with extracted text.
- **Plain text** → the text logic below.

Each content-skill does its own (delegated) fetch/transcription/OCR — route, don't fetch inline.

### Text: object-or-mentions
Two cases, decide which:
- **The whole text IS one object** — "Renovate the kitchen — 3 quotes" (`project`). → classify its type, create it, set relations, link.
- **The text MENTIONS objects but isn't one** — "Priya thinks ICICI will move on the export deal." → don't objectify the sentence; **find the objects inside it** (Priya, ICICI, the deal) and **wikilink them in place**, keeping the line as a linked log entry.
Use `classify-object-type` for types, `link-objects` to connect.

## Rules
- **Not everything becomes a new object — follow the recorded handling rule.** Check `99 System/_system/classification-learnings.md` first: the user may have chosen that some kinds of input (often touchpoints — meetings, calls, interactions) are logged as **linked entries in the daily note** rather than as dedicated objects. If so, append the entry to today's note and wikilink the people/projects involved (backlinks give them their timeline); don't create an `event` object. Honor whatever representation the user set per kind.
- **Write in the user's voice.** Any prose you put into the resulting objects (summaries, notes, context, log lines) is first person, as if the user wrote it — per `99 System/_system/writing-style.md`. A captured email about a meeting becomes "Met Priya — she'll send reports by Fri," not "The user met Priya."
- **Never silently delete.** Triage relocates and structures; the user can always trace back.
- **When ambiguous, ask in one line** rather than guessing the user's intent — but make the obvious calls yourself.
- **Apply minimalism** (`architecture.md`): default to a field/relation/inline-task before inventing a new type. A captured to-do is a checkbox, not a file.
- **Batch and summarize.** After triaging a backlog, give the user a 3–5 line summary: what was created, what was linked, what needs their decision.
