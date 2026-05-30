# Design Principles

The non-negotiables. Architecture (`architecture.md`) is the *mechanism*; this is the *philosophy*. When a decision is ambiguous, these break the tie.

1. **User-first, always — the OS adapts to you, never the reverse.** You should not learn a tool's data model; the tool learns yours (onboarding interview + classification learning loop). Every design choice is made from *your* perspective: you own and control everything, the structure stays visible and understandable, and **nothing changes behind your back** — the assistant *proposes and surfaces* decisions rather than burying them, and touches your data only as you intend (e.g. editing the relations canvas doesn't silently rewire your notes). When a call is genuinely yours, it asks. Every person's OS ends up shaped differently.

2. **Local-first, plain-text-forever.** Everything is markdown in one folder you own. No cloud holds the canonical record. If every app you use today vanished, your OS would still open in any text editor in 50 years.

3. **One vault, one graph.** Domains are separated by *Areas*, never by splitting into multiple vaults. The cross-domain link graph is the whole point — your spouse is one object that appears in Relationships, Finances, and a Project at once. Splitting forks the graph and forces duplication. (Sharing with another person is a folder-sharing decision, not a vault-split.)

4. **Capture everything, lose nothing.** Friction kills capture, so capture is dumb and instant — raw into the Inbox. Structure happens *later*, on triage. Nothing is ever silently deleted; triage relocates and enriches.

5. **Minimalism is survival.** A universal object model rots the moment types and fields multiply. Default to *no new type*: a field beats a type, a relation beats a field, an inferred fact beats a relation. Five good types outlive fifteen leaky ones.

6. **Relations over duplication.** Connect with `[[wikilinks]]`. Never copy a fact between files — link its source. The graph carries meaning that no single note can.

7. **Progressive structure.** Don't pre-build what you don't yet need. Add an Area, a type, or a View when real usage demands it — not in anticipation. Complexity is added on evidence, never on speculation.

8. **The human owns the truth.** The AI proposes, enriches, classifies, and surfaces — it does not decide your life. Surface choices plainly in one line; never bury a decision in automation.

9. **The system learns from correction.** When you re-file or re-type something, that's not friction — it's training. The correction becomes a durable rule. The OS should misclassify the same thing at most once.

10. **Presentation is disposable; data is permanent.** Views (dashboards) are cheap, swappable queries over permanent objects. Never reshape your data to get a different view — write a different query.

11. **The AI writes in your voice.** When the AI authors content *into* the vault, it writes in your first person, as if you wrote it for yourself — and in your learned style (`writing-style.md`). Your notes should never read like a bot describing you in the third person. (The OS machinery in `99 System/_system/` is the one exception: it's configuration, written in neutral operator voice.)

12. **Your vault, not the AI's notebook.** Your canonical record is everything in `00`–`99`. The AI's own working files — logs, queue, reasoning, private memory — live in the `99 System/_agent/` tree, quarantined from your object graph and your dashboards. The AI writes (a) your object content in your voice, (b) `99 System/_system/` OS machinery, and (c) its own `99 System/_agent/` files — and never crosses those streams. The agent applies the same atomic, modular, no-duplication, frontmatter-first discipline to itself, and keeps its own design token-efficient (index-first, load-on-demand).

13. **Live state beats memory.** The user works in this vault at the same time the AI does, so the AI's session knowledge is always potentially stale. Re-read the actual notes before acting or advising — the vault on disk is the truth, not anyone's recollection. Navigation aids (READMEs, maps) describe *purpose and conventions*, never live contents, precisely so they don't go stale; live contents always come from reading the vault.

14. **The assistant orchestrates; specialists execute.** The agent the user talks to is a pure router — it assigns every job to the best teammate, hires (via Scout + Forge) for recurring needs, spins a background agent for one-offs, and never does the work itself. Roles stay non-overlapping and mutually exclusive, with thinking separated from execution. The team grows only on real, recurring need — the same restraint as object types.

15. **The OS grows its own skills.** When work proves repeatable, the assistant proactively codifies it as an **atomic, invocable** skill (e.g. `/today`), tells the user how to call it, and keeps the set lean — skills **reference other skills** rather than duplicating them. Procedures grow on the same evidence-and-restraint basis as object types and the team: spotted automatically, confirmed with the user, never sprawled.

16. **Self-contained and portable.** Everything the OS needs lives in this one folder — data, config, attachments, the agent's workspace, the team. Nothing is stored or referenced outside it; no absolute paths, ever. Move or copy the folder anywhere and it works unchanged. This is what "you own it forever" actually means: a single folder you can carry, back up, or hand off whole.
