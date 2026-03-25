# CLAUDE.md — Your Business Brain Conventions

This file tells any AI assistant how to work inside your vault. It's the handshake between you and the machine.

---

## Vault Structure

- `00-Soul/` — Core identity files. Who you are, what you sell, who buys, how you sound.
- `01-Decisions/` — Strategic decisions with dates. Why you chose what you chose.
- `02-Research/` — Market intelligence, competitor analysis, trend data.
- `03-Outputs/` — Generated content: ads, emails, proposals, landing pages.
- `04-Daily/` — Daily logs. What happened, what you learned, what changed.

## Skills

All work runs through terminal skills in `.claude/skills/`:
- `/setup` — Initialize a new client vault
- `/extract` — Soul Mining interviews (soul, audience, offer, voice)
- `/import` — Mine existing documents (proposals, emails, website copy) into Soul files
- `/generate` — Create outputs from Soul files (ads, emails, posts, proposals)
- `/enrich` — Deepen thin Soul files with follow-up questions
- `/audit` — Check vault health
- `/scout` — Cross-reference context against market signals
- `/update` — Pull latest Codify skills and system updates (never touches client data)

## File Conventions

- **Frontmatter is required.** Every file starts with YAML frontmatter:
  ```yaml
  ---
  type: soul | decision | research | output | daily
  status: active | draft | archived
  date: YYYY-MM-DD
  ---
  ```
- **Use Obsidian links.** Write `[[soul]]` not `[soul](soul.md)`. Double brackets create the knowledge graph.
- **Cross-reference everything.** When a decision relates to your audience, link it: `[[audience]]`. This builds the compound loop.
- **Date your files.** Decisions and research use format: `YYYY-MM-DD-topic-slug.md`

## Writing Rules

- Lead with the point. No throat-clearing.
- Use bullet points over paragraphs where possible.
- Include "Why" sections in every decision file.
- Keep daily notes short — 3-5 bullets max.
- Preserve the client's exact language during extraction. Clean up grammar only if unclear. Do NOT rewrite their voice.

## Folder Routing

When creating new files:
- Strategic choices → `01-Decisions/`
- Market data, competitor intel, trends → `02-Research/`
- Generated content (ads, emails, proposals) → `03-Outputs/`
- Daily reflections and session logs → `04-Daily/`
- Never modify `00-Soul/` files casually — these are your foundation. Enrich deliberately via `/enrich`.

## The Compound Loop

Your vault gets smarter because:
1. You capture decisions and research daily
2. Those files link back to your Soul files
3. AI reads the full graph before generating anything
4. Outputs improve because context compounds
5. Monthly review hardens the best insights into permanent Soul files

---

*This file is read by Claude Code, ChatGPT, Gemini, or any AI that opens this folder. It makes them work like they know your business.*
