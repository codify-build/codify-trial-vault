---
name: optimise
description: "Analyse what's working across your outputs, research, and CRM data, then recommend context file updates. Closes the feedback loop — your vault gets smarter over time."
---

# /optimise — Close the Feedback Loop

Analyses patterns across everything in your vault — outputs, research, deals won and lost, competitor intel — and recommends specific updates to your context files. This is how your vault compounds. Run it weekly and your outputs get measurably better.

## Before Running

Read EVERYTHING silently:
1. All files in `00-Context/` — current state of each context file
2. All files in `01-Decisions/` — recent decisions and CRM actions
3. All files in `02-Research/` — competitor intel, lead research, market trends
4. Recent files in `03-Outputs/` — what's been generated lately

## What to Analyse

### 1. Pattern Recognition
Scan across all vault activity and identify:

**Winning patterns:**
- Which pain points keep appearing in won deals? (from `01-Decisions/`)
- Which ad hooks or email subject lines were used for successful outreach?
- Which competitor weaknesses have you been exploiting?
- What language do prospects use most when they engage?

**Losing patterns:**
- What's common among lost deals?
- Which objections keep coming up? Are they addressed in `audience.md`?
- What competitor advantages are you not countering?
- Where is your messaging falling flat?

**Gaps:**
- Pain points mentioned in research but missing from `audience.md`
- Competitor positioning not reflected in your differentiation
- Testimonials or proof points you have but haven't captured in `soul.md`
- Offer improvements mentioned in conversations but not in `offer.md`

### 2. Context File Health Check
For each context file, assess:

| File | Check |
|------|-------|
| `soul.md` | Are recent wins and testimonials captured? Is the origin story current? |
| `audience.md` | Do pain points match what actual prospects are saying? Any new segments? |
| `offer.md` | Does pricing match reality? Is the guarantee still accurate? New deliverables? |
| `voice.md` | Does recent output match the voice rules? Any drift? |

### 3. Competitive Position Drift
If `/spy` reports exist in `02-Research/`:
- Have competitors changed their positioning since last scan?
- Are they now targeting your audience differently?
- Have they adjusted pricing or offers?
- Flag anything stale (competitor research older than 30 days)

## Output Format

Present findings as a brief report — not a document, just a conversation:

**What's working:**
- 2-3 bullet points on patterns driving results

**What needs attention:**
- 2-3 bullet points on gaps or drift

**Recommended updates:**
For each recommendation, show:
1. Which context file to update
2. What specifically to change (exact text)
3. Why — what evidence supports this change
4. Ask: "Want me to make this update?"

## Making Updates

If the user approves an update:
- Make the change to the context file
- Update the `last-updated` field in frontmatter
- If the file status was `draft`, check if it should move to `active`
- After updating, ask: "This change affects your [ads/emails/content/site]. Want me to regenerate any of those?"

This connects to `/sync` — if context files change, downstream outputs should update too.

## Save the Analysis

Save to `01-Decisions/[YYYY-MM-DD]-optimise-review.md`:

```yaml
---
type: decision
category: optimisation
date: [today]
last-updated: [today's date and time]
context_files_updated: [list of files changed]
patterns_identified: [count]
---
```

Brief summary of what was found and what was changed.

## When to Run

- **Weekly**: ideal cadence — enough activity to spot patterns, frequent enough to stay sharp
- **After a big win or loss**: capture what worked or didn't while it's fresh
- **After running /spy**: competitive intel should immediately feed back into context
- **Before a campaign**: make sure context is current before generating outputs

## The Compound Effect

This is the skill that makes the vault a living system instead of a static document store. The cycle:

1. `/extract` or `/enrich` → build context
2. `/ad`, `/email`, `/content`, `/site` → generate outputs from context
3. `/ghl` → push to CRM, send emails, manage pipeline
4. `/spy`, `/leads`, `/research` → gather intelligence
5. **`/optimise`** → feed everything back into context files
6. Repeat — every cycle, outputs get better because context got better

## Tone Rules

- Be specific — "add this exact pain point to audience.md" not "consider updating your audience file"
- Back every recommendation with evidence from the vault
- Don't overwhelm — max 5 recommendations per session
- Celebrate what's working before pointing out gaps
- Frame updates as compound interest — "this small change will improve every future output"
