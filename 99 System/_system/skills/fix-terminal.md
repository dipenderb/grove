# Skill: Fix Terminal Rendering

**Trigger:** The user reports garbled or misaligned terminal output — `�` glyphs, broken box-drawing, stray escape codes, smeared spinners — **while running the assistant inside an embedded terminal** (e.g. Obsidian's *Terminal* plugin). Only relevant when such a terminal plugin is in use.
**Goal:** Make the embedded terminal render cleanly, using **OS-native fixes** for whichever OS the user is on.

## Step 1 — Detect the OS
You're running in it: check platform (`$env:OS` / `uname -s` / the environment). Apply the matching block below. Don't apply Windows fixes on macOS, etc.

## Step 2 — Apply fixes

### First: the Obsidian Terminal plugin settings (most common cause)
If they're using Obsidian's *Terminal* plugin, check these before anything OS-level — they fix most garbling:
- **Renderer → DOM** (Settings → Terminal). The WebGL/Canvas renderers often produce junk glyphs; DOM renders reliably.
- **Default profile → Integrated** (so the in-app terminal launches the right shell).
Then reload the terminal panel and re-test. If still garbled, apply the OS-native encoding fixes below.

### OS-native fixes

### Windows (PowerShell in the Terminal plugin)
Most Windows rendering issues are **encoding** (wrong codepage) or **ConPTY**:
1. **UTF-8 codepage + encoding** (fixes `�` and broken box characters):
   - `chcp 65001`
   - `$OutputEncoding = [Console]::OutputEncoding = [System.Text.UTF8Encoding]::new()`
   - Persist: add those two lines to the PowerShell profile (`$PROFILE`).
2. **Terminal plugin settings** → enable **Windows ConPTY** (gives proper ANSI/PTY handling); if it's already on and *causing* the smearing, toggle it off and retry. Set the profile to PowerShell/pwsh.
3. **Font:** set the plugin's terminal font to one with box-drawing + powerline glyphs (Cascadia Mono/Code, or any Nerd Font).

### macOS / Linux
1. **UTF-8 locale:** ensure `LANG`/`LC_ALL` are UTF-8 (e.g. `export LANG=en_US.UTF-8`); persist in the shell rc.
2. **TERM:** `export TERM=xterm-256color` if colors/cursor are off.
3. **Font:** set a glyph-capable font in the plugin (a Nerd Font).

### Any OS
- If a tool's heavy TUI (animated spinners, full-screen redraws) is what smears, prefer its plain/non-interactive output mode.

## Step 3 — Verify & persist
Print a test line with a box char and an emoji (e.g. `┌─┐ ✅`) and confirm it renders. Then **persist** the fix (shell profile + plugin settings) so it survives restarts — a fix that doesn't survive a reload isn't fixed.

> This is a setup/troubleshooting skill, not part of the data model. It touches the shell profile and the plugin's settings, never the user's vault content.
