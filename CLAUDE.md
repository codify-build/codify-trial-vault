# CLAUDE.md — Context Architecture Conventions

This file tells any AI assistant how to work inside this vault. Read it before doing anything.

---

## Who This Vault Belongs To

A senior leader with deep domain expertise. Their institutional knowledge — frameworks, beliefs, judgment calls — is the most valuable asset in this vault. Respect it. Preserve their voice. Never genericize their expertise.

## Vault Structure

- `00-Context/` — Core identity files. Who they are, what they sell, who buys, how they sound.
- `01-Decisions/` — Strategic decisions with dates and reasoning.
- `02-Research/` — Market intelligence, competitor analysis, industry signals.
- `03-Outputs/` — Generated content: ads, emails, proposals, campaigns.
- `04-Daily/` — Session notes and observations.

## Skills

All work runs through skills in `.claude/skills/`:
- `/setup` — Personalize a new vault
- `/extract` — Context Extraction interviews (soul, audience, offer, voice)
- `/import` — Mine existing documents (proposals, emails, website copy) into Context files
- `/generate` — Create outputs from Context files (ads, emails, posts, proposals)
- `/enrich` — Deepen thin Context files with follow-up questions
- `/audit` — Check vault health
- `/scout` — Cross-reference context against market signals
- `/update` — Pull latest Codify skills and system updates (never touches client data)

## File Conventions

- **Frontmatter is required.** Every file starts with YAML frontmatter:
  ```yaml
  ---
  type: context | decision | research | output | daily
  status: active | draft | archived
  date: YYYY-MM-DD
  last-updated: YYYY-MM-DD HH:MM
  ---
  ```
- **Always update `last-updated`** when modifying any file. Use the current date and time (24h format). This tells the client when each file was last touched.
- **Use Obsidian links.** Write `[[soul]]` not `[soul](soul.md)`. Double brackets create the knowledge graph.
- **Cross-reference everything.** When a decision relates to the audience, link it: `[[audience]]`. This builds the compound loop.
- **Date your files.** Decisions and research use format: `YYYY-MM-DD-topic-slug.md`

## Writing Rules

- Lead with the point. No throat-clearing.
- Use bullet points over paragraphs where possible.
- Include "Why" sections in every decision file.
- Keep daily notes short — 3-5 bullets max.
- **Preserve the client's exact language during extraction.** Clean up grammar only if unclear. Do NOT rewrite their voice — capture it. Their 30 years of judgment shows up in how they phrase things.

## Folder Routing

When creating new files:
- Strategic choices → `01-Decisions/`
- Market data, competitor intel, trends → `02-Research/`
- Generated content (ads, emails, proposals) → `03-Outputs/`
- Session notes → `04-Daily/`
- Never modify `00-Context/` files casually — these are the foundation. Enrich deliberately via `/enrich`.

## The Compound Loop

This vault gets smarter because:
1. Decisions and research are captured continuously
2. Those files link back to Context files
3. AI reads the full graph before generating anything
4. Outputs improve because context compounds
5. Monthly review hardens the best insights into permanent Context files

**Context > Prompts. Always.**

---

*This file is read by Claude Code, ChatGPT, Gemini, or any AI that opens this folder. It makes them work like they know the business.*
