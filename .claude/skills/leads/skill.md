---
name: leads
description: "Find and qualify prospects using your vault context. Research companies, score fit against your audience profile, and push qualified leads to GHL."
---

# /leads — Find & Qualify Prospects

Finds people who match your ideal client profile, researches them, scores their fit, and pushes the best ones into your CRM. Every lead is qualified against YOUR context — not generic criteria.

## Before Running

Read these files silently:
1. `00-Context/audience.md` — Your ideal client profile, pain points, industries, failed alternatives
2. `00-Context/offer.md` — What you sell, pricing, who it's for
3. `00-Context/soul.md` — Your positioning, expertise, credibility markers

Scan `02-Research/` for existing prospect research and competitive intel.

## What to Ask

1. "What kind of leads are you looking for? A specific industry, role, company size, or problem?"
2. "How many do you want? (I'll find 10 by default)"
3. "What's the goal — cold outreach, warm introduction, or just research for now?"

## How It Works

### 1. Build the Qualifier
From `audience.md`, extract:
- Industry markers
- Company size signals
- Pain point indicators
- Failed alternative signals (what they've tried that didn't work)
- Budget indicators from `offer.md` pricing

### 2. Research
Use WebFetch and WebSearch to find prospects:
- Search LinkedIn, company websites, industry directories
- Look for signals that match `audience.md` pain points
- Check their current solutions — are they using a competitor from `02-Research/`?
- Look for trigger events: hiring, funding, product launches, complaints

### 3. Score Each Lead

Score 1-10 based on fit against `audience.md`:

| Score | Meaning |
|-------|---------|
| 8-10 | Strong fit — matches pain points, budget, and profile |
| 5-7 | Possible fit — some signals, needs more research |
| 1-4 | Weak fit — don't waste time |

For each lead, document:
- **Company**: name, website, size, industry
- **Contact**: decision-maker name, role, LinkedIn
- **Fit score**: 1-10 with reasoning
- **Pain signals**: specific evidence they have the problem you solve
- **Trigger**: why NOW is the right time to reach out
- **Angle**: personalised hook based on their specific situation + your `offer.md`

### 4. Push to CRM
For leads scoring 7+, ask: "Want me to add these to your CRM?"

If yes, use `/ghl` to:
- Create contact with name, email, company
- Tag as "prospect", "lead-research", and industry tag
- Add to prospecting workflow if one exists
- Create opportunity in pipeline with estimated value

### 5. Draft Outreach
For top leads, offer: "Want me to draft a personalised message for any of these?"

If yes:
- Use `voice.md` for tone
- Reference their specific pain point
- Connect to your specific solution from `offer.md`
- Keep it short — 3-4 sentences max
- Save draft to `03-Outputs/[YYYY-MM-DD]-outreach-[company].md`

## Output Format

Save to `02-Research/[YYYY-MM-DD]-leads-[industry-or-query].md`:

```yaml
---
type: research
category: lead-research
date: [today]
last-updated: [today's date and time]
query: [what they searched for]
leads_found: [count]
qualified: [count scoring 7+]
source_files:
  - 00-Context/audience.md
  - 00-Context/offer.md
---
```

## The Feedback Loop

After research, check findings against context files:

- "3 of these leads mentioned [problem] — it's not in your `audience.md` pain points. Want to add it?"
- "Most prospects in this space are using [competitor tool]. Want me to run `/spy` on them?"
- "The decision-maker title is usually [role], not [role in audience.md]. Worth updating your audience profile?"

## Tone Rules

- This is a business development assistant, not a data dump
- Lead with the best opportunities — don't bury gold in a spreadsheet
- Be honest about weak leads — "these 3 are a stretch" saves time
- Frame outreach angles in terms of the prospect's problem, not your client's product
- Never suggest spammy tactics — quality over quantity
