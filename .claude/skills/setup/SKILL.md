---
name: setup
description: "Personalize a new client's vault and start their first extraction. Conversational — the client just answers questions."
---

# /setup — Personalize Your Business Brain

The client already has the vault open in Obsidian. The folder structure, plugins, and skills are all in place. This skill personalizes the vault for their business and kicks off their first Context Extraction session.

## Procedure

### 1. Welcome and Gather Info

Say:
"Welcome to Codify. I'm going to set up your Business Brain — a secure vault for your expertise that gets smarter over time. I just need to ask you a couple of things."

Ask these one at a time:

1. **"What's your business name?"**
   → Store for personalizing files

2. **"What's your name?"**
   → Store for personalizing files

### 2. Personalize the Vault

Do this silently — no need to narrate each step.

1. Update `CLAUDE.md` — replace any placeholder references with the client's business name
2. Update `README.md` — personalize with client name and business name
3. Write the tier file:
   ```bash
   echo "explore" > 00-Context/.tier
   echo "0" > 00-Context/.extractions
   ```
4. Update frontmatter dates in Context files to today's date
5. Set up the update channel (silently — client never sees this):
   ```bash
   # Ensure upstream remote exists for future skill updates
   git remote get-url upstream 2>/dev/null || git remote add upstream https://github.com/mike-scott-darwin/codify-vault-template.git
   ```

Say: "Your vault is personalized. Everything you see in the sidebar on the left is yours."

### 3. Quick Tour (30 seconds)

Say:
"Here's what you're looking at:

- **00-Context** — This is where your core identity lives. We're about to fill these in.
- **01-Decisions** — Every strategic decision you make goes here.
- **02-Research** — Market intelligence and competitor data.
- **03-Outputs** — Everything the system generates for you — ads, emails, proposals.
- **_dashboards** — Open 'context-power' to see your vault health at any time.

Everything syncs to your secure backup automatically. You don't need to think about it."

### 4. Start First Extraction

Say: "Your vault is ready. Let's fill it with your expertise. I'm going to ask you some questions about your business. Just talk naturally — there are no wrong answers."

Then immediately run `/extract soul`.

## Tone

- **Simple.** No jargon. No "repo," "git," "commit," "push," "CLI."
- **Confident.** "Your vault is personalized" not "I'm going to try to set up..."
- **Fast.** Don't over-explain. They need to see their files, not understand the architecture.
- **Reassuring.** "Everything is backed up securely. You own all of this."

## Error Handling

| Situation | What to say |
|-----------|------------|
| Context files missing | Recreate them silently from the template structure, then continue. |
| Client gets confused | "No worries. You don't need to do anything technical. I'm handling everything. Just answer my questions." |
| Client asks about backups | "Everything syncs automatically to a secure backup. You don't need to think about it." |

## What the Client Walks Away With

After 15 minutes:
- Vault personalized with their business name
- Context file populated from the extraction conversation
- Auto-sync running silently in the background
- All skills available via the chat pane
- Dashboards showing their context health
