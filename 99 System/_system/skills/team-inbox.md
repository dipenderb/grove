# Skill: Team Inbox

**Invoke:** `/team`
**Trigger:** Items present in `01 AI Team Inbox/`, the user adds a line to the shared `@AI Team Board.md`, or the user hands the team work in chat ("have the team research/draft/build X"). Also checked at session start (§0).
**Goal:** Turn work the user hands the AI team into tracked, routed, delivered results — visibly, from the shared board.

## Steps
1. **Capture it on the Board.** For each request (a file in `01 AI Team Inbox/`, a Board line, or a chat ask), add/confirm an entry under **Queued** on `@AI Team Board.md` — one line, plain `-`, what's wanted + any link to the source file.
2. **Classify the work:**
   - **A vault change** ("add these contacts", "file this note") → it's normal capture/triage, not a deliverable. Run the right skill, file as proper objects, link. Skip `02`.
   - **A produced artifact** (research, draft, summary, generated file) → it's a deliverable for review → continues below.
3. **Route** per the dispatch algorithm (`../../_agent/Team/README.md`): surgical → do it yourself; heavy/bulk → **Tend**; domain expertise → a fitting teammate, or Scout researches + Forge hires. Move the Board line to **In-progress**, noting who.
4. **Do / oversee the work**, in the user's voice (`writing-style.md`). Read live state first; never clobber the human (concurrent-edit rule).
5. **Deliver to `02 AI Team Deliverables/`** — one clearly-named file per deliverable, linked back to its source. `02` is **review-only**: leave it there; do **not** auto-file it into the vault (promote to a vault object only if the user asks).
6. **Close the loop:** move the Board line to **Recently delivered** with a link to the `02` file; **summarise in chat** (what was produced, where, any decision needed); run workspace upkeep (`agent-log.md`).
7. **Clear the intake:** the original request in `01 AI Team Inbox/` is processed → archive it (`99 System/Archive/AI Team Inbox/`) so the inbox trends empty. Never delete.

## Rules
- **The Board is the shared truth** — keep Queued/In-progress/Delivered current so the user can see and steer mid-flight. Plain `-` bullets (no `- [ ]`) so team work stays out of the user's personal task lists.
- **`01` is intake, `02` is review, the Board is status** — don't conflate them. Your private reasoning/logs stay in `99 System/_agent/`.
- **Surgical vs heavy:** a quick one-step ask you just do (and still log on the Board); a big/bulk/long job goes to Tend.
- Distinct from `capture-triage` (which handles *life capture* in `00 Inbox/` into the user's graph). This handles *work the user delegates to the team*.
