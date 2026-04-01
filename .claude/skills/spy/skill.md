---
name: spy
description: "Competitive intelligence — scrape competitor ads, websites, and social profiles. Saves findings to 02-Research/ and flags what to update in your context files."
---

# /spy — Competitive Intelligence

Scrape and analyse your competitors so your context files stay sharper than theirs. Every insight feeds back into your vault — your ads get better, your positioning gets tighter, your copy hits harder.

## Before Running

Read these files silently:
1. `00-Context/audience.md` — Who you serve (to compare against competitor targeting)
2. `00-Context/offer.md` — What you sell (to compare positioning and pricing)
3. `00-Context/voice.md` — How you sound (to identify differentiation opportunities)

Scan `02-Research/` for any existing competitor research to build on, not duplicate.

## What to Ask

"Who do you want to spy on? Give me a competitor name, website, or industry."

Then ask: "What do you want to know — their ads, their website copy, their pricing, their social, or everything?"

## Actions

### 1. Ad Library Scrape
Use WebFetch to pull from Meta Ad Library:
- Search `https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=ALL&q=[competitor name]`
- Extract: ad copy, headlines, CTAs, creative themes, how long ads have been running
- Analyse patterns: What pain points do they lead with? What objections do they address? What's their hook style?
- Flag any messaging angles NOT in your `audience.md` — these are blind spots

### 2. Website Scrape
Use WebFetch on the competitor's website:
- Extract: headline, subhead, positioning statement, pricing, guarantee, testimonials
- Map their page structure: what sections do they use, in what order?
- Compare against your `offer.md`: where are they stronger? Where are you?
- Pull exact quotes from their testimonials — what are their customers actually saying?

### 3. Social Scrape
Use WebFetch on their LinkedIn, X/Twitter, or other public profiles:
- What content gets engagement? Topics, formats, posting frequency
- What language do their followers use in comments?
- What gaps exist — topics they're NOT covering that you could own?

### 4. Pricing & Positioning Analysis
- Map their offer tiers, pricing, and what's included
- Compare to your `offer.md`
- Identify: are they competing on price, value, exclusivity, or speed?
- Where can you outposition them?

## Output Format

Save to `02-Research/[YYYY-MM-DD]-spy-[competitor-name].md`:

```yaml
---
type: research
category: competitive-intel
date: [today]
last-updated: [today's date and time]
competitor: [name]
website: [url]
source_files:
  - 00-Context/audience.md
  - 00-Context/offer.md
---
```

Structure the report:

**Overview** — Who they are, what they sell, who they target
**Ad Analysis** — Key themes, hooks, CTAs, estimated spend patterns
**Website Analysis** — Positioning, copy structure, proof points
**Social Analysis** — Content strategy, engagement patterns
**Pricing** — Tiers, comparison to your offer
**Blind Spots** — Things they emphasise that you don't cover in your context files
**Opportunities** — Gaps you can exploit

## The Feedback Loop

After saving the report, check the findings against context files and recommend updates:

- "They're hitting [pain point] hard in their ads but it's not in your `audience.md`. Want me to add it?"
- "Their guarantee is stronger than yours. Worth updating `offer.md`?"
- "Their testimonials mention [outcome] — do your clients get that result too? If so, let's capture it."
- "They're not talking about [your strength] at all — that's a positioning gap you should own."

Ask permission before updating any context file. Show what would change.

## Tone Rules

- Frame as intelligence, not imitation — "here's what they're doing" not "here's what to copy"
- Business language — "their positioning", "their messaging", not "their H1 tag" or "their meta description"
- Be direct about where competitors are stronger — the client needs truth, not flattery
- Always end with actionable next steps, not just observations
