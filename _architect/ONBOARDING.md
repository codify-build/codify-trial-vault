# Architect Onboarding Guide

How to onboard a new client with zero friction.

---

## Before the Call (5 min)

1. **Personalize the installer:**
   Open `_architect/install-codify.command` and set:
   - `VAULT_NAME` → client's business name (lowercase, hyphens)
   - `GITHUB_TEMPLATE` → the template repo URL

2. **Send the installer to the client:**
   Email or DM with this message:

   > "Before our call, download this file and double-click it. It takes about 2 minutes and sets everything up. You don't need to do anything else."

   Attach: `install-codify.command`

---

## On the Call (45 min)

### First 5 min — Verify Setup

1. Ask them to open Obsidian — they should see the vault
2. If plugins aren't trusted: "Click 'Enable' on that popup"
3. Have them open the terminal pane: `Cmd+P` → "Terminal: Open Terminal"
4. In the terminal, type `claude` to start Claude Code
5. Verify you can see the vault files in Obsidian's sidebar

### Next 35 min — Extraction

Run the full extraction sequence:

```
/extract soul       → 7 questions (~10 min)
/extract audience   → 5 questions (~7 min)
/extract offer      → 5 questions (~7 min)
/extract voice      → 5 questions (~7 min)
```

After each extraction, point out the file populating in Obsidian above. The visual feedback is the "wow" moment.

### Last 5 min — Tour + Next Steps

1. Open `_dashboards/context-power.md` — show them their vault health
2. Open the Graph View (`Cmd+P` → "Graph View") — show the knowledge connections
3. Explain the compound loop: "Every decision you log, every piece of research — it all feeds into better outputs"
4. Schedule the first Brain Sync (monthly review)

---

## After the Call

1. **Set up GitHub backup:**
   From your own terminal (not the client's):
   ```bash
   cd [client-vault-path]
   gh repo create [client]-sovereign-vault --private --source=. --push
   ```
   The Obsidian Git plugin will auto-sync from here.

2. **Run first generation:**
   ```
   /generate ad       → Show them what their context produces
   /generate post     → LinkedIn post from their Soul files
   ```
   Send them the outputs. This proves the system works.

3. **Run first audit:**
   ```
   /audit
   ```
   Share the report. Identify enrichment opportunities for the next session.

---

## The Client's Ongoing Experience

| Action | How | When |
|--------|-----|------|
| Browse files | Open Obsidian | Anytime |
| Check dashboards | Open `_dashboards/context-power.md` | Weekly |
| Add a daily note | Create file in `04-Daily/` | Daily (optional) |
| Log a decision | Create file in `01-Decisions/` | As needed |
| Get AI outputs | Book a session — architect runs `/generate` | As needed |
| Deepen Soul files | Book a session — architect runs `/enrich` | Monthly |
| Vault health review | Brain Sync session — architect runs `/audit` | Monthly |

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Installer won't run | Right-click → Open → "Open anyway" (macOS Gatekeeper) |
| Homebrew install hangs | Client may need to enter their Mac password |
| Claude Code not found | Run `npm install -g @anthropic-ai/claude-code` in terminal |
| Obsidian Git not syncing | Set up GitHub repo from architect's machine, then configure remote |
| Client added files in wrong folder | Move them during Brain Sync — no harm done |
| Client is overwhelmed | Simplify: "Just open Obsidian and browse. I handle the rest." |
