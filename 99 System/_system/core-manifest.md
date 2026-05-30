# Core / User Manifest

Defines what an **update** may touch. **The contract: updates refresh only the CORE (shared machinery) and NEVER touch the USER layer (your life + your personalization). Updates are backward-compatible — additive only; they never rename, move, or delete a user's folders, types, objects, or settings.**

## CORE — refreshed by `/update` (the shipped machinery)
- `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `README.md`, `START HERE.md`, `VERSION`, `LICENSE`, `.gitignore`
- `99 System/_system/`: `principles.md`, `architecture.md`, `conventions.md`, `properties-and-tags.md`, `relations.md`, `object-model.canvas`, `obsidian-setup.md`, `README.md`, `core-manifest.md`
- `99 System/_system/skills/` — all skill files (new skills are **added**; existing ones refreshed)
- `99 System/_system/template-library/` — the reference templates
- `99 System/_agent/`: `AGENT.md`, `conventions.md`, `Team/README.md`, `Team/Scout.md`, `Team/Forge.md`, `Team/Tend.md` (the standing-team definitions)

## USER — never touched by an update (yours)
- **All content folders & files:** `00 Inbox/`, `01 AI Team Inbox/`, `02 AI Team Deliverables/`, `@AI Team Board.md`, every onboarding-created type folder (`10 Projects/`, `20 People/`, `@Dashboards/`, `@Tasks/`, the Journal, …) and everything in them.
- **Your archive & files:** `99 System/Archive/`, `99 System/Files/`, `99 System/Templates/` (populated for your kept types).
- **Your personalized machinery:** `99 System/_system/` → `object-types.md`, `PROPERTIES.md`, `config.md`, `writing-style.md`, `classification-learnings.md`, `onboarding-state.md`.
- **Your assistant & its memory:** `99 System/_agent/` → `identity.md` (your assistant's name/persona), `logs/`, `memory/`, and any `Team/<custom hire>.md` you added.
- **Your settings:** `.obsidian/` (Obsidian owns these; an update never overwrites them).

## Rules for any future release
- **Additive, not destructive.** A new version adds skills/principles/relations; it does not remove or rename what a user already has. If a concept is superseded, the old path keeps working and the change is opt-in.
- **No forced migrations.** If a structural improvement needs the user's data to move, the update *proposes* it (the user approves) — it never moves data silently.
- **Personalized files are merge-aware.** For `object-types.md` / `PROPERTIES.md` etc., an update may *suggest* new default rows but never overwrites the user's edits.
- **Version is the gate.** Compare `VERSION` to the latest release; apply only the CORE diff.
