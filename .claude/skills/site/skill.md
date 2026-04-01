---
name: site
description: "Build a complete website from your Context files. Generates a Next.js site with copy, styling, and structure derived from your vault."
---

# /site — Build Your Website

Creates a full, deployable website from your Context files. Not a template — every word comes from your vault.

## Before Building

Read these files in order:
1. `00-Context/soul.md` — Who you are, your story, credentials, and positioning
2. `00-Context/audience.md` — Who you serve, their pain points, voice of customer
3. `00-Context/offer.md` — What you sell, pricing, guarantee, delivery method
4. `00-Context/voice.md` — How you sound, tone, words you use and avoid

Also scan:
- `01-Decisions/` — Recent strategic decisions that affect messaging
- `02-Research/` — Market research, competitor intel, testimonials
- `03-Outputs/` — Existing landing pages, ads, emails for consistency

If any Context file has `status: draft` or is mostly empty, warn:
"Your [file] is thin. The site will be generic in places. Run `/enrich [file]` first for better results. Continue anyway?"

## What to Ask

1. "What's the primary goal of this site — book a call, capture leads, sell directly, or establish authority?"
2. "Do you have a domain name? (I can set up deployment after)"
3. "Any pages beyond the homepage you want? (e.g., About, Results, Pricing, FAQ)"

## What to Build

Create a Next.js project with Tailwind CSS using this architecture:

### Site Config
Create a `src/site-config.ts` that pulls ALL copy into one file — headlines, subheads, CTAs, testimonials, stats. Every string comes from the Context files, not invented.

### Homepage Sections
Build as separate components in `src/components/`:

1. **Hero** — Headline from `offer.md` transformation promise. Subhead from `audience.md` pain points. One CTA button.
2. **Problem** — 3 pain cards from `audience.md#Pain Points` with stats if available from `02-Research/`.
3. **Mechanism** — How it works in 3-4 steps from `offer.md#Delivery`.
4. **Proof** — Results, stats, before/after from `02-Research/` and `soul.md#External Perception`.
5. **Testimonials** — From `soul.md#External Perception` or `02-Research/`. Real quotes only.
6. **Product** — What's included from `offer.md`. Pricing if applicable.
7. **FAQ** — Common objections from `audience.md#Objections` reframed as questions.
8. **CTA** — Final call to action matching the site goal.
9. **Footer** — Simple with copyright and contact.

### Additional Pages
If requested, create as separate routes under `src/app/`:
- `/about` — Founder story from `soul.md#Origin Story`
- `/results` — Expanded proof with all testimonials and stats
- Any other pages the client needs

### Design
- Dark theme by default (clean, modern, professional)
- Mobile-first responsive design
- Smooth scroll-triggered animations (fade in, slide up)
- Typography: system font stack, clamp() for responsive sizing
- Accent color: ask the client or derive from their brand

### Key Patterns
- All copy in `site-config.ts` — easy to update without touching components
- Each section is its own component — clean separation
- No external dependencies beyond Next.js and Tailwind
- Static export compatible for simple hosting
- Can switch to serverless if API routes needed later

## Deployment

After building, ask: "Ready to put this live?"

If yes:
1. Initialize a git repo
2. Help them connect to Vercel (free tier)
3. Set up their custom domain if they have one

## Save Output

Save the site project alongside the vault (not inside it):
- `../[business-name]-site/` — The full Next.js project

Log the build in `03-Outputs/[YYYY-MM-DD]-site-build.md` with frontmatter:

```yaml
---
type: output
format: website
date: [today]
last-updated: [today's date and time]
source_files:
  - 00-Context/soul.md
  - 00-Context/audience.md
  - 00-Context/offer.md
  - 00-Context/voice.md
goal: [book-call | lead-capture | direct-sale | authority]
pages: [list of pages built]
---
```

Include a summary of what was built and where the project lives.

## Tone Rules

- Do NOT mention technical details unless asked. No "Next.js", "Tailwind", "components" — just "your website."
- Frame everything in business terms: "your homepage", "your about page", "your call-to-action"
- This is a senior business owner. They care about what the site says and does, not how it's built.
- If the context is thin, say so honestly — "your site will be stronger after you deepen your context files."
