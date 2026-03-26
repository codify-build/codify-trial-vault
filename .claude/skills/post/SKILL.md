---
name: post
description: "Generate a LinkedIn post from your Context files."
---

# /post — Generate LinkedIn Post

Creates a LinkedIn post that sounds like you, not a content mill.

## Before Generating

Read these files in order:
1. `00-Context/soul.md` — Who you are
2. `00-Context/audience.md` — Who you serve
3. `00-Context/offer.md` — What you sell
4. `00-Context/voice.md` — How you sound

Also scan `01-Decisions/` and `02-Research/` for recent entries.

If any Context file has `status: draft` or is mostly empty, warn:
"Your [file] is thin. Output quality will improve if you run `/enrich [file]` first. Generate anyway?"

## What to Generate

Ask: "What angle? A belief, a story, a lesson, or a contrarian take?"

- **Belief:** Lead with a contrarian belief from `soul.md`. Back it with a specific example.
- **Story:** Tell a client story (anonymized) that proves the transformation in `offer.md`.
- **Lesson:** One tactical insight from `soul.md#Institutional Knowledge`.
- **Contrarian take:** Challenge conventional wisdom in their industry.

Format:
- Strong opening line (hook)
- 150-250 words
- Line breaks between thoughts (LinkedIn format)
- No hashtags unless the client uses them
- End with a question or clear point — not a CTA

## Save Output

Write to `03-Outputs/[YYYY-MM-DD]-post-[slug].md` with frontmatter:

```yaml
---
type: output
format: post
date: [today]
last-updated: [today's date and time]
source_files:
  - 00-Context/soul.md
  - 00-Context/audience.md
  - 00-Context/offer.md
  - 00-Context/voice.md
---
```
