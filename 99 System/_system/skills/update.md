# Skill: Update Grove

**Invoke:** `/update`
**Trigger:** The user asks to update Grove / check for a new version.
**Goal:** Bring the **core machinery** to the latest release **without ever disturbing the user's content, structure, or personalization.** Backward-compatible, additive only.

## Steps
1. **Check version.** Read local `VERSION`; fetch the latest release tag from the Grove repo. If local ≥ latest, tell the user they're current and stop.
2. **Show what's changing — and confirm.** Summarise the release notes in one or two lines. Updates are CORE-only; say so. Don't proceed without a nod.
3. **Snapshot first.** If the vault is a git repo, commit the current state (or note the restore point); otherwise copy the CORE files to `99 System/Archive/_pre-update-<version>/`. Never update without a way back.
4. **Apply CORE only.** Overwrite **only** the paths listed under *CORE* in `99 System/_system/core-manifest.md`. **Touch nothing in the USER layer** — content folders, `@AI Team Board.md`, archive, the personalized `_system` files (`object-types.md`, `PROPERTIES.md`, `config.md`, `writing-style.md`, `classification-learnings.md`, `onboarding-state.md`), `_agent/identity.md`, `logs/`, `memory/`, custom hires, or `.obsidian/`.
5. **Additive merges, never overwrites, for personalized files.** If the release adds new *default* object-types, relations, or allowed values, **propose** adding them to the user's `object-types.md` / `relations.md` / `PROPERTIES.md` — apply only on approval, appending, never replacing their edits.
6. **No forced migrations.** If a change would move/rename any user data, **propose** it with a clear before/after and do it only if the user agrees. Default = leave their structure exactly as is.
7. **Stamp & report.** Update `VERSION`, append the change to the agent log, and tell the user in 3–5 lines: what core changed, what (if anything) they may want to opt into, and confirm their data/structure is untouched.

## Rules
- **Backward-compatible is the law.** A user on an old version must keep working after an update with zero manual fixes.
- **CORE refreshes; USER persists.** When unsure whether a path is core or user, treat it as **user** (don't touch) and ask.
- **Verify, never claim.** Confirm the new files actually landed and the user layer is intact before reporting success.
