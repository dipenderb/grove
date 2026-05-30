# Skill: Process Screenshot

**Invoke:** `/process-screenshot`
**Trigger:** A captured **image / screenshot / photo** — or invoked by `process-daily-note` / `capture-triage` when one is detected.
**Goal:** Extract meaning from an image and file it; keep the image.

## Steps
1. **OCR** the image — *delegated* to an OCR/vision tool / background agent.
2. Branch on what it is:
   - **Business card** → create a `person` (and `company`) from the details, linked.
   - **Otherwise** → store the image as a `file`/`resource` with the extracted text (so it's searchable), linked; set `area`.
3. Run the *object-or-mentions* logic (`capture-triage.md`) on the extracted text — find and wikilink any objects mentioned.
4. **Keep the original image file.**

Report what was created and linked.
