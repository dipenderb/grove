# Skill: Import Existing Files

**Trigger:** The user wants to bring existing notes/files into the OS — usually right after onboarding, or anytime later. **Not during the interview itself.**
**Goal:** Fold an existing pile into the *established* structure through the normal pipeline, so nothing drifts.

**Why after onboarding:** you can only sort into a structure once it's settled. Importing into a still-forming structure creates churn and forces premature types. Onboarding *samples* a few files to inform the design; this skill does the *bulk*, carefully.

## Drift guards (the reason this is its own skill)
- **Map to what exists, first.** Classify every import against the established types, Areas, relations, and recognition signatures. The OS shape is fixed — files conform to it, not the reverse.
- **Same pipeline, no shortcuts.** Everything routes through capture → `classify-object-type` → `link-objects` → file. No special import path that skips the discipline.
- **No type sprawl on import.** Never auto-create a type per file. If *many* files share a pattern that fits no existing type, surface it **once** through `new-object-type`'s 2-of-4 gate — the user decides. Default is fit-to-existing.
- **Dedupe.** Match people/companies/projects to existing objects; merge, never duplicate.
- **Preserve originals.** Never destroy a source file. Archive raw imports to `99 System/Archive/imports/<date>/` so nothing is ever lost.
- **Batch + review.** Import in small batches; show results from the first batch early so misclassifications are caught and feed `classification-learnings.md` before processing the rest.

## Steps
1. **Scope.** Ask what to import (a folder, a vault export, specific files) and roughly how much.
2. **Stage.** Bring sources into `00 Inbox/` (or a temp import area) as captures — don't process in place.
3. **Triage in batches** (~20 at a time): classify via recognition signatures → create/link objects → file. Non-markdown (docs, PDFs, images) → `resource`/`file` objects with extracted text.
4. **Checkpoint after batch 1.** Show what was created / linked / skipped, plus any proposed new type. Get a thumbs-up or corrections (corrections → `classification-learnings.md`). Adjust, then continue.
5. **Dedupe pass.** Merge duplicate people/companies surfaced across batches.
6. **Report.** Counts by type, what was archived, and anything left as unresolved captures for the user to decide.

## Rules
- **Token-efficient:** frontmatter-first, batch, link don't restate.
- **User's voice** for any content written (`writing-style.md`).
- **When in doubt on a file, leave it as a capture and flag it** — never force-fit. Forcing a misfit is exactly the drift this skill exists to prevent.
