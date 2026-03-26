---
name: ad
description: "Generate ad copy (Facebook/Instagram/Meta) from your Context files."
---

# /ad — Generate Ad Copy

Creates ad copy that sounds like you, speaks to your buyer, and sells your offer.

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

- 3 hook variations (pattern-interrupt opening lines)
- Primary copy body (150-200 words)
- Call to action
- Suggested headline and description for Meta ad format

The copy must:
- Use the client's voice and signature phrases from `voice.md`
- Reference the specific transformation from `offer.md`
- Address the audience's pain points using their language from `audience.md`
- Reflect core beliefs from `soul.md`

## Save Output

Write to `03-Outputs/[YYYY-MM-DD]-ad-[slug].md` with frontmatter:

```yaml
---
type: output
format: ad
date: [today]
last-updated: [today's date and time]
source_files:
  - 00-Context/soul.md
  - 00-Context/audience.md
  - 00-Context/offer.md
  - 00-Context/voice.md
---
```
