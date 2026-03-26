---
name: start
description: "Welcome back screen for Codify. Shows vault state, recent changes, and what to do next."
---

# /start — Welcome to Codify

When the client runs `/start`, do the following:

## 1. Read the Vault State

Before showing anything, silently read:
- All files in `00-Context/` — check `status` and `last-updated` in frontmatter
- Recent files in `03-Outputs/` — last 3 by date
- Recent files in `01-Decisions/` — last 3 by date
- Count of files in each folder

## 2. Determine If This Is a First Visit or Return

**First visit** — all Context files have `status: draft` or are template-only (contain `<!-- -->` comment placeholders with no real content).

**Returning** — at least one Context file has `status: active` or `status: compounding`.

## 3. Display the Right Welcome

### If First Visit:

**Welcome to Codify**

This is your Context Architecture — a secure vault where your expertise compounds over time. Everything you share here stays here. The AI reads it all before generating anything, so your outputs reflect your judgment, not generic advice.

**Start here:**
- Type `/extract soul` to capture your core identity
- Or `/import` if you have existing material (proposals, website copy, emails) — it's faster

### If Returning:

**Welcome back.**

Then show a brief status report:

**Your Context Files:**
- For each file in `00-Context/`, show: name, depth (Getting there / Solid / Deep based on status field), and last-updated
- Flag any file not updated in 14+ days as "could use a refresh"

**Since your last session:**
- List any new files in `03-Outputs/` or `01-Decisions/` created since the oldest `last-updated` across Context files
- If no new files, say "No new outputs since your last session."

**Recommended next step:**
- If any Context file has zero outgoing `[[links]]`: "Your [file] has no connections to other files. Run `/enrich [file]` to link it up — this makes your outputs sharper."
- If any Context file is still `status: draft`: "Your [file] could go deeper. Run `/enrich [file]` to strengthen it."
- If all Context files are `status: compounding`: "Your context is strong. Ready to create? Try `/ad`, `/email`, `/content`, or `/proposal`."

**What you can do:**

| Command | What It Does |
|---------|-------------|
| `/extract` | Build your context files through conversation |
| `/import` | Mine existing documents into context files |
| `/enrich` | Go deeper on any context file |
| `/ad` | Create ad copy |
| `/email` | Create email sequences |
| `/content` | Create content for any platform |
| `/proposal` | Create a client proposal |
| `/landing` | Create landing page copy |
| `/audit` | See your vault health |
| `/scout` | Find market opportunities using your context |
| `/brief` | Summary of vault health and recommended focus |

## Tone Rules

- Do NOT mention git, GitHub, terminal, CLI, API, MCP, skills, or any technical infrastructure
- This client is a senior leader with deep expertise. Speak to their intelligence, not their technical ability.
- Keep it concise. No filler. Lead with what matters.
- If returning, the status report IS the value. They open Obsidian, type `/start`, and immediately know where they stand and what to do next.
