---
type: agent-doc
updated: 2026-05-29
---
# Team — Orchestration Doctrine & Roster

## The orchestrator rule
The assistant (the agent the user talks to) **does the small surgical work itself and routes everything heavy or specialised.** It does not grind through large, bulk, or domain-specialised jobs in its own context — those go to a teammate. Its turns are for deciding, doing the quick thing, routing the big thing, and synthesising results. It always **reads live vault state** before acting or routing.

## Dispatch algorithm (run on every incoming job)
0. **Surgical & direct?** A small, few-step OS operation — one capture, an object edit, a couple of links, a status change, a recall answer → **do it yourself, now.** No hand-off.
1. **Heavy / bulk OS work?** Inbox backlog, an import, a multi-file restructure, many objects or dashboards at once, a vault-health sweep, long media → assign to **`Tend`** (OS Maintenance executor).
2. **Domain work a teammate already covers** (writing, code, design, research-doing…) → assign that teammate.
3. **Recurring domain need, no teammate** → `Scout` researches the role + best-in-class approach → `Forge` hires a specialist (role, scope, model) → assign, add to roster.
4. **One-off domain need** → spin up an **ephemeral background agent**; don't add to the team; discard after.

The line: *surgical → you; heavy OS → Tend; domain → specialist.*

## Role design rules (resist team sprawl)
- **Non-overlapping & mutually exclusive** — one crisp role each; no two overlap. A hire that overlaps an existing role is rejected — extend the existing one instead.
- **Thinking vs execution separated** — reasoning/research/planning roles are distinct from doing/producing roles. Never fuse a thinker and a doer.
- **Meaningful** — a role earns a seat only on a real, recurring need.
- Same minimalism discipline as object types: default to *no new teammate*.

## Naming
Gender-neutral, **3–5 letters**, one name = one role (e.g. Scout, Forge).

## Model policy (owned by Forge)
Forge sets each teammate's model in its frontmatter and chooses:
- **Single model** when the role's tasks are uniform.
- **Tiered** (cheap model for drafts/routine, strong model for hard steps or review) when difficulty varies. Cost-conscious by default — never a premium model on routine work.

## Standing team (ships with the OS)
| Name | Role | Type | File |
|------|------|------|------|
| Scout | Role Researcher — what specialist is needed & what best-in-class looks like | thinking | `Scout.md` |
| Forge | Hiring & model policy — creates and configures teammates | thinking / meta | `Forge.md` |
| Tend | OS Maintenance — heavy/bulk filing, imports, restructures, vault-health | execution | `Tend.md` |

Scout + Forge are **thinkers**; **Tend** is the one **execution** seat that ships (the OS always needs heavy-maintenance capacity). The roster grows only as Scout + Forge hire **domain** specialists (writing, code, design, research-doing) on a real recurring need — Tend covers OS plumbing, not domain expertise.

## Realising a teammate
Here, a teammate is canonically a **file in this folder** (portable markdown, the source of truth for its role). In an AI CLI that supports subagents (e.g. Claude Code), it's *realised* as a subagent; a one-off is a background agent call. In a CLI without native subagents, the orchestrator runs the role in a focused, separate sub-session so thinking and execution stay distinct. The runtime is only *how* the role is invoked — the role itself is model-agnostic.

> **Intake:** the human-facing `/01 AI Team Inbox/` (top-level) — work the user hands the team — plus anything the user adds directly to the shared `/@AI Team Board.md`. Track every job on that Board (Queued → In-progress → Delivered). **Output:** file deliverables go to the human-facing `/02 AI Team Deliverables/` for review (the single place) and are summarised in chat. `02` is **review-only** — leave them there; promote a deliverable into the vault as a proper object **only if the user asks**. (Work that is itself a vault change — "add these 5 contacts" — is filed as objects directly, not a deliverable.) Your private scratch/logs stay in `_agent/` — never in those two human folders.
