---
type: agent-doc
updated: 2026-05-29
---
# 99 System/Files — Attachment Store

The **default home for binary attachments** — pasted images, PDFs, voice notes, scanned cards. Set Obsidian's *default location for new attachments* to this folder (see `../obsidian-setup.md`) so attachments never scatter next to notes and the content folders (`00`–`99`) stay clean.

## What lives here vs. not
- **Here:** raw files, embedded from notes via `![[filename]]`.
- **Not here:** a *tracked* file (one you want metadata/links on) → make a `resource` object in the Resources folder that points to the file. The binary is storage; the `resource` is the object.

## Archiving
When an attachment is no longer referenced by any note, move it to `99 System/Archive/Files/`. Don't delete — archive.

> This README describes the folder's **purpose**, not its contents. For what's actually in here, read the folder live.
