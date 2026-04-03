---
name: gate
description: "Skill tier gating — checks client tier before running locked skills. Reads tier from vault config."
---

# Skill Gating System

Every skill checks the client's tier before executing. The tier is stored in the vault's config file.

## Tier Config

The file `00-Context/.tier` (or `.tier` in the vault root) stores the client's tier:

```
explore
```

Valid values: `explore`, `architect`, `focus`, `sovereign`

The architect sets this during `/setup`. It's a plain text file — no YAML, no complexity.

## How Gating Works

Every skill SKILL.md includes a tier requirement in its frontmatter. Before executing, check:

1. Read `00-Context/.tier` (fall back to `.tier` in vault root if not found)
2. Compare against the skill's required tier
3. If the client's tier is sufficient, run the skill
4. If not, show the upgrade message

## Tier Hierarchy

```
explore < architect < focus < sovereign
```

- `explore` can run explore-tier skills only
- `architect` can run explore + architect skills
- `focus` can run explore + architect + focus skills
- `sovereign` can run all skills

## Skill Map

### Explore (Free)

| Skill | Description |
|-------|-------------|
| `/start` | Guided onboarding — first run experience |
| `/extract` | 3 free extractions (soul, audience, offer), then shows upgrade prompt |
| `/import` | Mine existing documents into Context files (counts as an extraction) |
| `/audit` | Vault health check (read-only) |

### Architect ($497/mo)

Everything in Explore (unlimited extractions), plus:

| Skill | Description |
|-------|-------------|
| `/extract` | Unlimited — all extractions, re-enterable |
| `/import` | Unlimited — no extraction cap |
| `/enrich` | Deepen existing Context files with follow-up questions |
| `/ad` | Generate ad copy (Meta/Facebook/Instagram) |
| `/email` | Generate email sequences (cold, warm, nurture) |
| `/content` | Generate content for any platform (LinkedIn, blog, newsletter, X/Twitter) |
| `/proposal` | Generate client proposal |
| `/landing` | Generate landing page copy |
| `/case-study` | Turn a client win into a formatted case study |
| `/follow-up` | Write a follow-up message after a call or meeting |
| `/objection` | Handle a sales objection using your context |
| `/pitch` | Elevator pitch, event intro, podcast bio, speaker page |
| `/research` | Research a prospect, competitor, market trend, or scan for opportunities |
| `/brief` | Morning brief — decisions, priorities, open threads |

### Focus ($1,497 + $497/mo)

Everything in Architect, plus:

| Skill | Description |
|-------|-------------|
| `/publish` | Distribute outputs to live channels |
| `/campaign` | Full pipeline — generate + distribute across channels |
| `/repurpose` | One piece of content → every channel |

### Managed Sovereign ($5,000 + $997/mo)

Everything in Focus, plus:

| Skill | Description |
|-------|-------------|
| `/security` | Vault security audit, red team simulation, hardening report |
| Sovereign infrastructure | Dedicated hosting, private repos, custom integrations |

### Architect-Only (Internal — Not Client-Facing)

These skills are used by Codify architects to manage client vaults. They do not appear in client-facing menus.

| Skill | Description |
|-------|-------------|
| `/update` | Pull latest Codify skills and system updates (never touches client data) |
| `/openclaw` | Engine orchestration and automation internals |
| `/gate` | This skill — tier enforcement logic |
| `/setup` | Initial vault provisioning and personalization |

## Upgrade Prompts

When a client tries a locked skill:

**Explore → Architect:**
"This skill is available on the Architect plan ($497/mo). You get unlimited extractions, AI-powered content generation, research, and proposal writing — all trained on your context. Want to upgrade? Talk to your Codify architect."

**Explore/Architect → Focus:**
"This skill is available on the Focus plan ($1,497 + $497/mo). You get done-for-you campaigns, multi-channel distribution, and content repurposing — all from a single input. Want to upgrade? Talk to your Codify architect."

**Any → Managed Sovereign:**
"This skill is available on the Managed Sovereign plan ($5,000 + $997/mo). You get dedicated infrastructure, security hardening, and white-glove management. Want to upgrade? Talk to your Codify architect."

## Extraction Limit (Explore Only)

For Explore tier, track extraction count in `00-Context/.extractions`:

```
2
```

Increment after each `/extract` or `/import` run. At 3, show:
"You've used your 3 free extractions. Your Context files are already improving your outputs — imagine what happens with unlimited extractions and full content generation. Upgrade to Architect to unlock everything."

## Model Assignment

Each tier gets a model that matches its value. The model is set in `.claude/settings.json`:

```json
{
  "model": "claude-haiku-4-5-20251001"
}
```

| Tier | Model | Why |
|------|-------|-----|
| **Explore** (Free) | `claude-haiku-4-5-20251001` | Fast, reliable, zero cost to client |
| **Architect** ($497/mo) | `claude-sonnet-4-6` | Stronger generation, better skill execution |
| **Focus** ($1,497/mo) | `claude-opus-4-6` | Best reasoning, complex campaigns |
| **Sovereign** ($5,000/mo) | `claude-opus-4-6` | Same model, sovereign infrastructure |

### How to upgrade the model

When a client upgrades tier, the architect updates `.claude/settings.json`:

```bash
# Example: upgrading to Architect
claude config set model claude-sonnet-4-6
```

Or edit `.claude/settings.json` directly:

```json
{
  "model": "claude-sonnet-4-6"
}
```

The template ships with Haiku as default. Upgrades happen during the tier change — one file, one line.

## Notes

- The `.tier` and `.extractions` files are dotfiles — hidden in Obsidian by default
- The architect sets the tier during `/setup` or manually
- Upgrading is just changing one word in `.tier` and one line in `settings.json` — no API calls, no license servers
- This is an honor system backed by the relationship, not DRM
- `/import` counts against the Explore extraction limit because it writes to Context files
