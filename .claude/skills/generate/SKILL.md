---
name: generate
description: "Generate high-fidelity outputs (ads, emails, proposals, posts) from your Context files. Context > Prompts."
---

# /generate — Output Generation from Context

Reads your Context files in `00-Context/` and generates business outputs that sound like you. The more complete your Context files, the better the output.

## Usage

```
/generate ad          → Facebook/Instagram ad copy
/generate email       → Cold or warm email sequence
/generate post        → LinkedIn post
/generate proposal    → Client proposal
/generate brief       → Morning brief from recent activity
/generate landing     → Landing page copy
```

## Procedure

### 1. Read the Reference Stack

Before generating ANYTHING, read these files in order:
1. `00-Context/soul.md` — Who they are
2. `00-Context/audience.md` — Who they serve
3. `00-Context/offer.md` — What they sell
4. `00-Context/voice.md` — How they sound

Also scan:
- `01-Decisions/` — Recent decisions (last 5 by date)
- `02-Research/` — Recent research (last 3 by date)

### 2. Check Depth

Before generating, assess Context file completeness:
- If any Context file is at Skeleton depth (< 200 bytes), warn:
  "Your [file] is thin. Output quality will improve if you run `/extract [file]` first. Generate anyway?"
- If all files are at Working+ depth, proceed.

### 3. Generate Output

Use the full reference stack as context. The output must:
- Use the client's voice (from `voice.md`)
- Reference their specific transformation (from `offer.md`)
- Address their audience's actual pain points (from `audience.md`)
- Reflect their core beliefs (from `soul.md`)
- Incorporate recent decisions if relevant

### 4. Save Output

Write generated content to `03-Outputs/` with format:
```
03-Outputs/[YYYY-MM-DD]-[type]-[slug].md
```

Include frontmatter:
```yaml
---
type: output
format: [ad|email|post|proposal|brief|landing]
date: [today]
source_files:
  - 00-Context/soul.md
  - 00-Context/audience.md
  - 00-Context/offer.md
  - 00-Context/voice.md
---
```

### 5. Before/After (Optional)

If the user asks, show the delta:
- Generate the same output WITHOUT reading Context files (generic)
- Show both side by side
- The difference is the proof that context > prompts
