---
name: funnel
description: "Generate and deploy marketing funnels at scale — landing pages, SEO pages, blog posts, email sequences, and ads — all from your Context files, deployed directly to GoHighLevel."
---

# /funnel — Build & Deploy Marketing Funnels at Scale

One command to generate entire marketing funnels from your Context files and deploy them live to GoHighLevel. This is Codify's highest-leverage skill — turning context into converting pages at scale.

## Usage

```
/funnel                         → Interactive — choose funnel type and topic
/funnel seo [topic]             → Generate SEO page batch for a topic/niche
/funnel launch [offer]          → Full launch funnel (landing + emails + ads)
/funnel blog [topic] [count]    → Batch-generate blog posts (default: 5)
/funnel retarget                → Retargeting funnel from existing outputs
/funnel status                  → Show deployed funnels and their assets
```

## Funnel Types

### 1. SEO Page Batch (`/funnel seo`)
Mass-produce SEO-optimized pages targeting long-tail keywords. This is how you build 50–100+ pages that convert cold traffic.

**Generates:**
- Keyword variations from your offer + audience context
- One blog post per keyword, each with unique angle
- Internal linking between posts
- CTA on every page pointing to your core offer

### 2. Launch Funnel (`/funnel launch`)
Full campaign funnel for a new offer, event, or push.

**Generates:**
- 1 landing page (hero, problem, solution, proof, CTA)
- 3 ad variations (pattern interrupt, problem-aware, proof-forward)
- 3-email nurture sequence
- 1 thank-you / confirmation page
- 1 LinkedIn post to announce

### 3. Blog Batch (`/funnel blog`)
Authority content at scale. Each post draws from your Context files so it sounds like you, not AI.

**Generates:**
- N blog posts (default 5, max 20 per batch)
- Each post has unique angle, internal links, and CTA
- All formatted as GHL-ready HTML

### 4. Retarget Funnel (`/funnel retarget`)
Builds retargeting assets from your existing outputs.

**Generates:**
- 3 retargeting ad variations referencing prior content
- 2 follow-up emails for non-converters
- 1 alternative-angle landing page

## Procedure

### Step 1: Load Full Context

Read in order:
1. All `00-Context/` files (soul, audience, offer, voice)
2. Last 5 `01-Decisions/` entries
3. Last 5 `02-Research/` entries
4. Last 10 `03-Outputs/` (to avoid duplicating existing content)

If any Context file has `status: draft` or is mostly empty, warn:
"Your [file] is thin. Funnel quality depends on rich context. Run `/enrich [file]` first? Or generate anyway?"

### Step 2: Define the Funnel

If no type specified, ask:
"What kind of funnel do you need?
1. **SEO** — Batch of keyword-targeted pages for organic traffic
2. **Launch** — Full funnel for a new offer (landing + ads + emails)
3. **Blog** — Authority blog posts at scale
4. **Retarget** — Re-engage people who didn't convert"

If no topic specified, ask:
"What's the topic or offer this funnel is built around?"

### Step 3: Keyword/Angle Research (SEO & Blog types)

For SEO and Blog funnels:
1. Extract core themes from `audience.md` pain points and `offer.md` transformation
2. Generate keyword variations: `[pain point] + [solution type] + [audience segment]`
3. Cross-reference against existing `03-Outputs/` to avoid duplication
4. Present the keyword/topic list for approval:

```
Here are 10 page targets I'd generate:

1. "How [audience] can [solve pain point] without [failed alternative]"
2. "[Industry] guide to [transformation] in 2026"
3. ...

Approve all, edit the list, or adjust the count?
```

### Step 4: Generate Assets

Generate all assets in sequence. Each asset reads the full Context and builds on previous assets in the funnel for consistency.

**For each page/post, generate:**

```html
<!-- GHL-ready HTML structure -->
<div class="funnel-page">
  <section class="hero">
    <h1>[Headline from offer.md transformation]</h1>
    <p>[Subheadline from audience.md pain point]</p>
    <a href="[CTA link]" class="cta-button">[CTA text]</a>
  </section>

  <section class="problem">
    <!-- 3 pain points from audience.md#Voice of Customer -->
  </section>

  <section class="solution">
    <!-- Approach from soul.md, framed as the answer -->
  </section>

  <section class="proof">
    <!-- Testimonials from soul.md#External Perception -->
  </section>

  <section class="cta">
    <!-- Single clear CTA matching the funnel goal -->
  </section>
</div>
```

**Tone:** Always match `voice.md`. No generic marketing speak.

**Internal linking:** Each page links to 2-3 related pages in the batch using `[[page-slug]]` references (converted to real URLs on deploy).

### Step 5: Save All Outputs

Save each asset to `03-Outputs/` with funnel metadata:

```yaml
---
type: output
format: funnel-page
funnel: [funnel-name-slug]
funnel-type: seo | launch | blog | retarget
page-index: 1
total-pages: 10
date: [today]
last-updated: [today's date and time]
keyword: "[target keyword]"
status: draft
source_files:
  - 00-Context/soul.md
  - 00-Context/audience.md
  - 00-Context/offer.md
  - 00-Context/voice.md
---
```

Also create a funnel manifest at `03-Outputs/[date]-funnel-manifest-[slug].md`:

```yaml
---
type: output
format: funnel-manifest
funnel: [funnel-name-slug]
funnel-type: seo | launch | blog | retarget
date: [today]
last-updated: [today's date and time]
total-assets: [count]
deployed: false
assets:
  - file: [filename]
    type: landing | blog | ad | email
    status: draft | deployed
    ghl-id: null
---
```

### Step 6: Review Package

Present the full funnel:

```
Your [type] funnel is ready:

[N] pages/posts generated
[N] email sequences
[N] ad variations

Files saved to 03-Outputs/

Options:
1. Review each asset individually
2. Deploy all to GoHighLevel now
3. Deploy selected assets only
4. Edit and regenerate specific assets
```

### Step 7: Deploy to GoHighLevel

On approval, deploy using MCP tools:

**Blog/SEO Pages → GHL Blog Posts:**
```
Use mcp__gohighlevel__create_blog_post for each page:
- title: from the page headline
- content: the full HTML
- description: meta description from the page
- urlSlug: keyword-based slug
- status: DRAFT (let user publish when ready) or PUBLISHED if they confirm
```

Before deploying blog posts:
1. Call `mcp__gohighlevel__get_blog_sites` to find available blog
2. Call `mcp__gohighlevel__get_blog_authors` for author ID
3. Call `mcp__gohighlevel__get_blog_categories` for category IDs
4. Call `mcp__gohighlevel__check_url_slug` for each slug to avoid conflicts

**Email Sequences → GHL Email Templates:**
```
Use mcp__gohighlevel__create_email_template for each email:
- title: email subject line
- html: the full email HTML
```

**Ad Copy → GHL Social Posts:**
```
Use mcp__gohighlevel__create_social_post for each ad variation
```

**Landing Pages → Output only (manual placement):**
Landing page HTML is generated and saved. Provide instructions:
"Landing page copy is ready in [filename]. To use in GHL:
1. Open your GHL Funnel Builder
2. Create a new page
3. Add a Custom HTML/Code element
4. Paste the generated HTML
Or use the copy sections individually in GHL's drag-and-drop builder."

### Step 8: Update Manifest

After deployment, update the funnel manifest with GHL IDs:

```yaml
assets:
  - file: 2026-03-27-funnel-seo-page-1.md
    type: blog
    status: deployed
    ghl-id: "abc123"
    url: "/blog/keyword-slug"
```

### Step 9: Report

```
Funnel deployed:

[N] blog posts created in GHL (status: DRAFT)
[N] email templates created
[N] social posts scheduled
[N] landing pages ready for manual placement

Funnel manifest: 03-Outputs/[date]-funnel-manifest-[slug].md

Next steps:
- Review drafts in GHL before publishing
- Run /funnel status to check deployment
- Run /campaign to promote these pages
```

## Scaling Notes

- **Batch limits:** Generate max 20 pages per `/funnel` call to maintain quality
- **Deduplication:** Always check existing `03-Outputs/` before generating to avoid duplicate content
- **Internal linking:** After deploying, update internal links with real GHL URLs
- **Iteration:** Run `/funnel seo [topic]` multiple times with different angles to build out a full content library
- **Tracking:** The funnel manifest tracks everything — use `/funnel status` to see what's deployed and what's still in draft
