---
name: gate
description: "Skill tier gating — checks client tier before running locked skills. Reads tier from vault config."
---

# Skill Gating System

Every skill checks the client's tier before executing. The tier is stored in the vault's config file.

## Tier Config

The file `00-Context/.tier` stores the client's tier:

```
explore
```

Valid values: `explore`, `architect`, `focus`

The architect sets this during `/setup`. It's a plain text file — no YAML, no complexity.

## How Gating Works

Every skill SKILL.md includes a tier requirement in its frontmatter. Before executing, check:

1. Read `00-Context/.tier`
2. Compare against the skill's required tier
3. If the client's tier is sufficient, run the skill
4. If not, show the upgrade message

## Tier Hierarchy

```
explore < architect < focus
```

- `explore` can run explore-tier skills only
- `architect` can run explore + architect skills
- `focus` can run all skills

## Skill Map

### Explore (Free)

| Skill | Description |
|-------|-------------|
| `/extract` | 3 extractions (soul, audience, offer), then shows upgrade prompt |
| `/score` | Context Power score |
| `/help` | How the system works |
| `/audit` | Basic vault health check (read-only) |

### Architect ($497/mo)

Everything in Explore (unlimited extractions), plus:

| Skill | Description |
|-------|-------------|
| `/extract` | Unlimited — all 4 files, re-enterable |
| `/enrich` | Deepen existing Context files |
| `/generate` | Create outputs (ad, email, post, proposal) |
| `/scout` | Opportunity scouting |
| `/think` | Research → decide → codify |
| `/brainstorm` | Generate ideas from reference stack |
| `/refine` | Improve existing output |
| `/voice` | Check content against voice.md |
| `/brief` | Morning brief |

### Focus ($1,497 + $497/mo)

Everything in Architect, plus:

| Skill | Description |
|-------|-------------|
| `/ads` | Full ad campaign pipeline |
| `/email` | Email sequence generation |
| `/newsletter` | Newsletter from research + decisions |
| `/organic` | Social content batch |
| `/blog` | Long-form blog post |
| `/vsl` | Video sales letter script |
| `/proposal` | Client proposal |
| `/report` | Executive report |
| `/seo` | SEO-optimized content |
| `/site` | Landing page copy |
| `/publish` | Distribute outputs to live channels |
| `/campaign` | Full pipeline — generate + distribute |
| `/repurpose` | One piece → every channel |

## Upgrade Prompts

When a client tries a locked skill:

**Explore → Architect:**
"This skill is available on the Architect plan ($497/mo). You get unlimited extractions, AI-powered generation, and opportunity scouting. Want to upgrade? Talk to your Codify architect."

**Explore/Architect → Focus:**
"This skill is available on the Focus plan. You get done-for-you campaigns, distribution to email/social/blog, and full output automation. Want to upgrade? Talk to your Codify architect."

## Extraction Limit (Explore Only)

For Explore tier, track extraction count in `00-Context/.extractions`:

```
2
```

Increment after each `/extract` run. At 3, show:
"You've used your 3 free extractions. Your Context files are already improving your outputs — imagine what happens with all 4 files fully enriched. Upgrade to Architect to unlock unlimited extraction."

## Notes

- The `.tier` and `.extractions` files are dotfiles — hidden in Obsidian by default
- The architect sets the tier during `/setup` or manually
- Upgrading is just changing one word in `.tier` — no API calls, no license servers
- This is an honor system backed by the relationship, not DRM
