# Skill: Process Audio

**Invoke:** `/process-audio`
**Trigger:** A captured **audio / voice note** — or invoked by `process-daily-note` / `capture-triage` when one is detected.
**Goal:** Turn speech into structured, linked objects without losing the recording.

## Steps
1. **Transcribe** the audio — *delegated* to a transcription tool / background agent.
2. Treat the transcript as **text** → run the *object-or-mentions* logic in `capture-triage.md` (the whole thing may be one object, or it may just mention objects to find and wikilink).
3. **Keep the audio file** (store it, link it) — never discard the original.

Report what was created and linked.
