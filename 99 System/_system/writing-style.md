# Writing Style Profile

When the AI writes content **into the vault** — a note body, a journal entry, a person's context, a project log — it writes **as the user, in first person**, as if the user wrote it for themselves. This file is the learned model of that voice. It is applied to every AI-authored *object* — and **not** to `99 System/_system/` machinery, which stays in neutral operator voice.

> Status: **DEFAULT — not yet learned.** Fill from the user's real writing during onboarding and refine from their edits.

---

## The voice rule
- **First person, for self.** "Met Priya at the clinic; she'll send the reports by Friday." Never "The user met Priya." A note should read as if the user typed it.
- **Their words, not yours.** Match the dimensions below. When unsure, default to plain, brief, and direct over ornate.
- Chat *to* the user (triage summaries, questions) stays in normal address — only **content written into objects** uses their first-person voice.

## Style dimensions (fill from real samples)
- **Tone** — _default: direct, plain, no filler._
- **Sentence length** — _default: short._
- **Vocabulary / jargon** — domain terms the user actually uses:
- **Abbreviations & shorthand** the user writes (e.g. "fwd", "eod", initials for people):
- **Capitalisation & punctuation quirks** (lowercase starts? em-dashes? no full stops in lists?):
- **Emoji / formatting habits** — _default: none._
- **Numbers & dates in prose** (e.g. "Fri", "5/6", "₹2L"):
- **Avoid** — words/phrases the user dislikes:

## Learning loop
- **Seed:** during onboarding, ask for a short writing sample (or read 2–3 existing notes/messages) and fill the dimensions above.
- **Refine:** whenever the user edits text the AI wrote, compare intent vs. their edit and update the relevant dimension with a dated note. Don't repeat a corrected habit.
- Keep this profile **short enough to apply** — a working model, not an essay.

## Samples
_(paste 1–3 short snippets the user actually wrote, for the AI to pattern-match against)_
