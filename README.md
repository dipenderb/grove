# 🌳 Grove

**Your own second brain — a personal operating system for your whole life and work, in one folder you own forever.**

Grove is local-first and made of plain Markdown. There's no app to sign up for, no company that can take it away, no lock-in. You talk to it in plain language; it captures your thoughts, files them as connected notes, and surfaces what matters — and it **builds itself around *your* life** by interviewing you the first time you open it.

> Every note is a typed object. Your domains (Health, Work, Relationships…) are Areas. You dump anything into an Inbox; Grove enriches it, files it, and links it into a growing mesh. Dashboards show you what matters. Nothing leaves your folder.

---

## Why Grove is different

- **It personalizes itself.** On first run it *interviews you* — your areas, what you track, how you capture — then builds the structure around your actual life. No template to bend yourself into.
- **The assistant maintains the graph for you.** Drop in a thought, a link, a photo of a card — Grove classifies it, creates the right notes, and links them. Your second brain doesn't rot.
- **You own everything.** Plain Markdown on your disk. Open it in any editor. Move the folder anywhere. Quit any time and your data is just… files.
- **Model-agnostic.** Works with Claude, Gemini, or any capable AI CLI. You bring your own — Grove itself costs nothing.

---

## Get started (zero-touch — ~5 minutes)

You need two things: **[Obsidian](https://obsidian.md)** (a free Markdown app) and an **AI CLI** you already use (e.g. [Claude Code](https://claude.com/claude-code) or Gemini CLI). Then:

### 1. Get your copy of Grove
- Click **“Use this template” → “Create a new repository”** (top of this page) — or just **“Code → Download ZIP”** and unzip it somewhere.
- This folder is *yours*. Rename it if you like (e.g. `My Grove`).

### 2. Open it in Obsidian
- Obsidian → **“Open folder as vault”** → pick your Grove folder.

### 3. Turn on the assistant (one-time)
- **Settings → Community plugins → Turn on community plugins**, then **Browse** and install **Terminal** (by *polyipseity*). *(Recommended too: **Dataview** for live dashboards, **Tasks** for reminders.)*
- **Settings → Terminal** → set **Renderer = DOM** and **Default profile = Integrated**.
- Open the terminal (command palette → “Terminal: Open terminal”) and type your AI command — **`claude`** (or `gemini`, `codex`).

### 4. Say hi
- In that terminal, just type **`hi`**. Grove starts a short interview and builds your system around you. That's it — you can't break anything.

> **Prefer VS Code?** Open the folder in VS Code, point Claude/Gemini at it, and say `hi`. Same result.

Full setup detail (plugins, mobile, the optional `obsidian` CLI) lives in **`99 System/_system/obsidian-setup.md`**.

---

## How it works (once you're in)

- **Capture** → drop anything in `00 Inbox/`; Grove files it into linked notes.
- **Hand work to the AI team** → drop a request in `01 AI Team Inbox/`; results come back in `02 AI Team Deliverables/` for review. The shared **`@AI Team Board.md`** shows what's queued, in progress, and done — and you can edit it too.
- **See at a glance** → Grove builds dashboards (per Area, per project) that stay live.
- **Ask it anything** → “what's open with Priya?”, “what did you change yesterday?” — it answers from your graph and its own daily logs.

You only ever see the folders that matter; the machinery lives in `99 System/` (greyed out).

---

## Your data, your rules

- 100% local Markdown. No account, no cloud dependency, no telemetry.
- Portable — move or copy the folder anywhere and nothing breaks.
- Sync it yourself if you want (Obsidian Sync, iCloud, Google Drive…). It's just files.
- **Bring your own AI** — Grove uses the AI CLI *you* run, so there's no cost to use Grove itself.

## Updates

Grove improves over time. Updates are **backward-compatible by design and never touch your content or structure** — they only refresh the shared machinery. Ask the assistant to **`/update`** and it pulls the latest core, leaving your notes, custom types, and personalization exactly as they are. (See `99 System/_system/core-manifest.md`.)

## Version & license

- **Version:** `v26.05.30-01` (see [`VERSION`](VERSION); scheme is `vYY.MM.DD-build`).
- **License:** [MIT](LICENSE) — free for everyone, forever. Fork it, share it, build on it.

---

*Already opened the folder? **[`START HERE.md`](START%20HERE.md)** walks you through the same steps from inside the app.*
