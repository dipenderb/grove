# _system — OS Machinery

Everything that *defines* how this OS works (not your life content). Neutral operator voice, not the user's. Map of what's here:

| File | What it is |
|------|------------|
| `principles.md` | The non-negotiable design philosophy (ties break here) |
| `architecture.md` | The object model — types, relations, minimalism, capture, views |
| `object-types.md` | Registry: what types exist, their fields + **recognition signals** |
| `relations.md` | Dictionary of relations — meaning + wikilink syntax |
| `template-library/` | Reference note templates (one per type); kept types are copied into `../Templates/` |
| `object-model.canvas` | **Canonical** map of how types relate (Obsidian Canvas) |
| `properties-and-tags.md` | Keeping properties & tags minimal and non-duplicative; property types (Text/List/Date) |
| `PROPERTIES.md` | Allowed values for controlled-vocabulary properties (keeps Obsidian suggestions clean) |
| `classification-learnings.md` | Append-only learned classification corrections |
| `writing-style.md` | The user's learned voice (for AI-authored content) |
| `config.md` | Runtime switches — `tasks_mode`, `dataview` |
| `conventions.md` | Naming, frontmatter, dates, linking, attachments |
| `obsidian-setup.md` | Plugin & setting setup for the human |
| `onboarding-state.md` | Whether the vault is personalized yet |
| `core-manifest.md` | What an `/update` may touch (CORE) vs never touch (USER) — backward-compat contract |
| `skills/` | Triggered operator protocols (see `../../AGENTS.md` table) |

This `_system/` folder lives inside **`99 System/`**, alongside its siblings:
| Sibling (in `99 System/`) | What it is |
|------|------------|
| `../Templates/` | Note templates for kept types only (ships empty; filled from `template-library/`) |
| `../Files/` | Default attachment store (binaries) |
| `../Archive/` | Inactive items, organised object-wise (`Archive/Projects/`, `Archive/Journal/YYYY/`) |
| `../_agent/` | The AI orchestrator's own workspace (see `../_agent/AGENT.md`) |

The full vault layout is mapped in `../../AGENTS.md` §3 (the canonical contract; `CLAUDE.md`/`GEMINI.md` are pointers to it).

> Describes purpose, not live contents — read files/folders directly for current state.
