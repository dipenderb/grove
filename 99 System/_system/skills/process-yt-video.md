# Skill: Process YouTube Video

**Invoke:** `/process-yt-video`
**Trigger:** A captured **YouTube (or other video) link** — or invoked by `process-daily-note` / `capture-triage` when one is detected.
**Goal:** Turn a video link into a linked `resource` with its substance captured, not just a URL.

## Steps
1. **Get the transcript / summary** — *delegated* to a transcript or web tool / background agent.
2. Create a `resource` (subtype `video`) with `url`, channel/source, and **key takeaways in the user's voice** (optionally a few timestamped points). Link, don't paste the whole transcript.
3. **Link** related objects (people, projects, areas) per `link-objects`; set `area`.
4. If it implies an action, add an inline `- [ ]` task.

Report what was saved.
