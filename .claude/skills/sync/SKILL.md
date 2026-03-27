---
name: sync
description: "Detect context changes and automatically regenerate all downstream outputs. The engine that makes the vault reactive — update a context file and everything downstream updates with it."
---

# /sync — Automatic Downstream Propagation

The core of Codify's compound loop. When a context file changes, /sync identifies every downstream output affected and regenerates them. Context flows down. Always.

## The Principle

```
Context Files (source of truth)
    ↓ changes detected
Dependency Map (what depends on what)
    ↓ affected outputs identified
Regeneration Queue (priority-ordered)
    ↓ each output regenerated with fresh context
Deployment Sync (live channels updated)
```

**Context is upstream. Everything else is downstream. Always.**

## Usage

```
/sync                    → Detect changes since last sync, regenerate affected outputs
/sync [context-file]     → Regenerate everything downstream of a specific context file
/sync --dry-run          → Show what would change without regenerating
/sync --deploy           → Regenerate AND push updates to live channels (GHL, email, social)
/sync status             → Show dependency map and last sync state
/sync history            → Show sync log
```

## Procedure

### Step 1: Detect Context Changes

Compare current context files against their `last-updated` timestamps in the sync manifest.

Check all upstream files:
1. `00-Context/soul.md` — identity, beliefs, frameworks
2. `00-Context/audience.md` — who you serve, their pain, their language
3. `00-Context/offer.md` — what you sell, pricing, guarantees
4. `00-Context/voice.md` — how you sound, tone rules, vocabulary
5. `01-Decisions/` — recent strategic decisions that shift positioning
6. `02-Research/` — new market intelligence

For each file, calculate a change hash:
- Read the file content
- Compare against the stored hash in `.claude/sync-manifest.yaml`
- If different → mark as changed

If no changes detected:
"All context files are in sync. No downstream updates needed. Last sync: [date]"

### Step 2: Build the Dependency Map

Every output in `03-Outputs/` has a `source_files` list in its frontmatter. Use this to build the dependency graph:

```yaml
# Which outputs depend on which context files
soul.md:
  - 03-Outputs/2026-03-25-ad-copy-spring.md
  - 03-Outputs/2026-03-25-landing-main.md
  - 03-Outputs/2026-03-27-funnel-manifest-seo.md

audience.md:
  - 03-Outputs/2026-03-25-ad-copy-spring.md
  - 03-Outputs/2026-03-25-email-cold-outreach.md
  - 03-Outputs/2026-03-27-funnel-manifest-seo.md

offer.md:
  - 03-Outputs/2026-03-25-landing-main.md
  - 03-Outputs/2026-03-26-proposal-client-x.md
```

### Step 3: Identify Affected Outputs

Cross-reference changed context files against the dependency map.

Present the impact report:

```
Context changes detected:

  CHANGED  00-Context/audience.md (last updated: 2026-03-27 14:30)
           Previous sync: 2026-03-25 09:00

Affected downstream outputs (4):

  1. 03-Outputs/2026-03-25-ad-copy-spring.md
     Depends on: audience.md, soul.md, offer.md
     Format: ad | Status: deployed (GHL social)
     
  2. 03-Outputs/2026-03-25-email-cold-outreach.md
     Depends on: audience.md, voice.md
     Format: email | Status: draft
     
  3. 03-Outputs/2026-03-27-funnel-seo-page-1.md
     Depends on: audience.md, offer.md, soul.md
     Format: funnel-page | Status: deployed (GHL blog)
     
  4. 03-Outputs/2026-03-27-funnel-seo-page-2.md
     Depends on: audience.md, offer.md, soul.md
     Format: funnel-page | Status: deployed (GHL blog)

Regenerate all 4 outputs? (yes / select specific / dry-run)
```

If `--dry-run` flag: show the report but don't regenerate.

### Step 4: Regenerate Outputs

For each affected output, regenerate using the SAME skill and parameters that created it:

**Read the output's frontmatter to determine the original skill:**

| Format | Regeneration Skill |
|--------|-------------------|
| ad | /ad |
| email | /email |
| landing | /landing |
| content | /content |
| proposal | /proposal |
| pitch | /pitch |
| case-study | /case-study |
| funnel-page | /funnel |
| funnel-manifest | /funnel |
| campaign-log | /campaign |
| blog | /content or /funnel |

**For each regeneration:**
1. Read ALL current context files (not just the changed one)
2. Read the existing output to preserve structure and intent
3. Regenerate the content with fresh context
4. Preserve the original frontmatter metadata (date, format, funnel association)
5. Update `last-updated` timestamp
6. Add sync metadata to frontmatter:

```yaml
last-synced: 2026-03-27 15:45
sync-trigger: audience.md
sync-generation: 3  # how many times this output has been regenerated
```

**Show diff for approval:**
For each regenerated output, show what changed:
```
Output: 03-Outputs/2026-03-25-ad-copy-spring.md

Changes:
- Headline: "Tired of generic marketing?" → "Tired of 8 tools and zero results?"
- Pain point #2: Updated to match new audience language
- CTA: Unchanged

Accept this update? (yes / skip / edit)
```

### Step 5: Deploy Updates (if --deploy flag or user approves)

For outputs that are already deployed to live channels:

**GHL Blog Posts:**
- Read the `ghl-id` from the output's frontmatter
- Use `mcp__gohighlevel__update_blog_post` to push the updated content

**GHL Email Templates:**
- Use `mcp__gohighlevel__update_email_template` with the stored template ID

**GHL Social Posts:**
- Use `mcp__gohighlevel__update_social_post` with the stored post ID

**Landing Pages:**
- Flag for manual update: "Landing page copy has been regenerated. Update your GHL funnel builder manually."

### Step 6: Update Sync Manifest

After sync completes, update `.claude/sync-manifest.yaml`:

```yaml
last-sync: 2026-03-27T15:45:00
sync-count: 14
context-hashes:
  soul.md: "abc123"
  audience.md: "def456"
  offer.md: "ghi789"
  voice.md: "jkl012"
outputs-synced:
  - file: 03-Outputs/2026-03-25-ad-copy-spring.md
    synced: 2026-03-27T15:45:00
    generation: 3
    deployed: true
  - file: 03-Outputs/2026-03-25-email-cold-outreach.md
    synced: 2026-03-27T15:45:00
    generation: 2
    deployed: false
```

### Step 7: Report

```
Sync complete:

  Context changes:  1 file (audience.md)
  Outputs updated:  4 of 4
  Deployed:         2 of 4 (blog posts updated in GHL)
  Manual updates:   0

  Next recommended sync: when you next update a context file
  Run /sync --dry-run anytime to preview changes

Sync manifest updated: .claude/sync-manifest.yaml
```

## Automatic Sync Triggers

The following skills should suggest running /sync after they modify context:

| Skill | Trigger |
|-------|---------|
| /extract | After creating or updating any Context file |
| /enrich | After enriching any Context file |
| /import | After importing new context from documents |
| /research | After adding research that changes positioning |

These skills should end with:
"Context updated. Run `/sync` to propagate changes to [N] downstream outputs."

## Sync Rules

1. **Never overwrite without approval** — always show the diff first
2. **Preserve intent** — regeneration keeps the original goal/topic, just updates the context-driven content
3. **Track lineage** — every output knows which context files built it and how many times it's been regenerated
4. **Batch efficiency** — if multiple context files changed, regenerate each output once (not once per context change)
5. **Deploy cautiously** — deployed outputs require explicit `--deploy` flag to push live updates
