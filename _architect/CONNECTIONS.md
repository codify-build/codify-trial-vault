# Architect Connection Guide

How the distribution skills (`/publish`, `/campaign`, `/repurpose`) connect to live channels. All connections run through the **architect's** Claude Code environment — the client never configures any of this.

---

## Architecture — The Codify Compound Loop

The system has three layers. The client sees one (Obsidian). The architect operates two (Claude Code + MCP tools). The server runs one autonomously (OpenClaw). Context flows through all three and compounds at every step.

```
╔══════════════════════════════════════════════════════════════════════════════════════════╗
║                              THE CODIFY COMPOUND LOOP                                   ║
╚══════════════════════════════════════════════════════════════════════════════════════════╝


  LAYER 1: CLIENT (Obsidian — Desktop)          LAYER 2: ARCHITECT (Claude Code + MCP)
  ─────────────────────────────────────          ─────────────────────────────────────────

  ┌──────────────────────────────────┐           ┌─────────────────────────────────────┐
  │  SOVEREIGN VAULT (GitHub/Forgejo)│           │  CLAUDE CODE (Terminal / Agent)      │
  │                                  │           │                                     │
  │  00-Context/                     │──────────>│  Reads ALL context before generating │
  │    soul.md      ◄──┐             │           │                                     │
  │    audience.md  ◄──┤ Cross-refs  │           │  Skills:                            │
  │    offer.md     ◄──┤ compound    │           │    /extract  ──> writes Context/    │
  │    voice.md     ◄──┘ over time   │           │    /enrich   ──> deepens Context/   │
  │                                  │           │    /import   ──> mines docs into    │
  │  01-Decisions/                   │           │                  Context/            │
  │    2026-03-26-pricing.md ────────│───┐       │    /ad       ──> writes Outputs/    │
  │    2026-03-25-positioning.md ────│───┤       │    /email    ──> writes Outputs/    │
  │                                  │   │       │    /content  ──> writes Outputs/    │
  │  02-Research/                    │   │       │    /proposal ──> writes Outputs/    │
  │    2026-03-26-competitor-x.md ───│───┤       │    /landing  ──> writes Outputs/    │
  │    2026-03-25-market-trends.md ──│───┤       │    /research ──> writes Research/   │
  │                                  │   │       │    /audit    ──> vault health check │
  │  03-Outputs/                     │<──┘       │    /brief    ──> morning summary    │
  │    ad-spring-2026.md             │           │                                     │
  │    email-cold-outreach.md        │           │  THE KEY: Every output is informed  │
  │    proposal-acme.md              │           │  by every context file. More context │
  │                                  │           │  = better outputs. That's the       │
  │  04-Daily/                       │           │  compound effect.                   │
  │    session notes                 │           │                                     │
  │                                  │           └──────────────┬──────────────────────┘
  │  _dashboards/                    │                          │
  │    Context Power (depth score)   │                          │ MCP CONNECTIONS
  │    What Needs Attention          │                          │ (Architect-side only)
  │    Reference Health              │                          │
  └──────────────────────────────────┘                          │
           │                                     ┌──────────────┴──────────────────────┐
           │  Obsidian Git                       │  DISTRIBUTION ENGINE                │
           │  auto-syncs                         │                                     │
           │  every 10 min                       │  Gmail MCP ────────> Email sends    │
           ▼                                     │  GoHighLevel MCP ──> Social posts   │
  ┌──────────────────────────────────┐           │                  ──> SMS campaigns  │
  │  GITHUB / FORGEJO (Backup)       │           │                  ──> Blog posts     │
  │                                  │           │  YouTube MCP ────> Transcript pull  │
  │  Version-controlled. Sovereign.  │           │  Gemini MCP ─────> Deep research   │
  │  Every change tracked. Portable. │           │                  ──> Image gen      │
  │  Client owns it. We manage it.   │           │  (Future) ───────> Substack         │
  │                                  │           │                  ──> Beehiiv         │
  └──────────────────────────────────┘           │                  ──> LinkedIn API   │
                                                 └─────────────────────────────────────┘


  LAYER 3: ALWAYS-ON ENGINE (Private Server — VPS)
  ─────────────────────────────────────────────────

  ┌────────────────────────────────────────────────────────────────────────────────────┐
  │  OPENCLAW — Runs while the client sleeps                                          │
  │                                                                                    │
  │  ┌─────────────────────────────┐     ┌──────────────────────────────────────────┐  │
  │  │  SCHEDULED JOBS             │     │  TELEGRAM BOT (@Codify_build_bot)        │  │
  │  │                             │     │                                          │  │
  │  │  5:30 AM  Morning Brief     │────>│  Ops Channel                             │  │
  │  │           Vault health      │     │    Morning brief lands on phone          │  │
  │  │           Open tasks        │     │    Staleness alerts                      │  │
  │  │           Competitor signals │     │    Vault health warnings                │  │
  │  │                             │     │                                          │  │
  │  │  2:00 AM  Deep Research     │────>│  Research Channel                        │  │
  │  │           Market signals    │     │    Overnight findings                    │  │
  │  │           Competitor moves  │     │    Positioning audits                    │  │
  │  │           Trend scanning    │     │    Market signal alerts                  │  │
  │  │                             │     │                                          │  │
  │  │  Hourly   Vault Backup      │     │  Content Channel                         │  │
  │  │           Git sync all      │     │    Draft review requests                 │  │
  │  │           client vaults     │     │    "Approve" / "Reject" / feedback       │  │
  │  │                             │     │    Posting confirmations                 │  │
  │  │  Weekly   Competitor Monitor│     │                                          │  │
  │  │           Track moves       │     │  General Channel                         │  │
  │  │           Alert on changes  │     │    Quick questions from phone            │  │
  │  │                             │     │    Idea capture (voice/text)             │  │
  │  │  Daily    Staleness Check   │     │    Routes to correct vault folder        │  │
  │  │           Flag old files    │     │                                          │  │
  │  └─────────────────────────────┘     └──────────────────────────────────────────┘  │
  │                                                                                    │
  │  HOW IT COMPOUNDS OVERNIGHT:                                                       │
  │                                                                                    │
  │  1. Engine reads today's new Research/ and Decisions/ files                        │
  │  2. Cross-references against Context/ files (soul, audience, offer, voice)         │
  │  3. Identifies patterns: "3 of 5 recent prospects are in HVAC at $20M"            │
  │  4. Writes summary to 02-Research/ with [[links]] back to Context/                │
  │  5. Morning brief includes the insight + recommended Context/ update               │
  │  6. Client wakes up. Opens Obsidian. The vault is smarter than yesterday.         │
  │                                                                                    │
  └────────────────────────────────────────────────────────────────────────────────────┘


╔══════════════════════════════════════════════════════════════════════════════════════════╗
║  THE COMPOUND EFFECT                                                                    ║
║                                                                                         ║
║  Week 1:   4 thin Context files. Generic outputs.                                      ║
║  Month 1:  Enriched Context + 10 Research files + 5 Decisions.                         ║
║            Outputs reference your frameworks by name.                                   ║
║  Month 3:  40+ files. Cross-referenced knowledge graph.                                ║
║            Ads use your buyer's exact language. Proposals cite your proof points.       ║
║  Month 6:  100+ files. Overnight research compounds automatically.                    ║
║            The vault knows your market better than your competitors know theirs.        ║
║  Year 1:   A digital twin of your professional judgment.                               ║
║            Every output sounds like you wrote it on your best day.                     ║
║                                                                                         ║
║  The system gets smarter because:                                                       ║
║    - Every /extract adds depth to Context/                                              ║
║    - Every /enrich adds [[cross-references]] between files                             ║
║    - Every /research adds market data that informs future outputs                      ║
║    - Every Decision logged becomes a reference point for future strategy               ║
║    - OpenClaw processes it all overnight — you wake up to a smarter vault              ║
║                                                                                         ║
║  Context > Prompts. Always.                                                             ║
╚══════════════════════════════════════════════════════════════════════════════════════════╝
```

The client creates context. The architect distributes it. OpenClaw compounds it overnight. The client never touches a third-party tool.

---

## MCP Servers Required

These must be configured in the **architect's** `~/.claude.json` — NOT in the client's vault.

### 1. Gmail

Sends emails directly from the architect's Gmail (or client's, if configured).

```json
"gmail": {
  "type": "stdio",
  "command": "node",
  "args": ["/opt/homebrew/lib/node_modules/@gongrzhe/server-gmail-autoauth-mcp/dist/index.js"],
  "env": {
    "GMAIL_OAUTH_PATH": "/path/to/.gmail-mcp/gcp-oauth.keys.json",
    "GMAIL_CREDENTIALS_PATH": "/path/to/.gmail-mcp/credentials.json"
  }
}
```

**Setup:** `npm install -g @gongrzhe/server-gmail-autoauth-mcp` then follow OAuth flow.

**Skills that use it:** `/publish email`, `/campaign`

### 2. GoHighLevel

Manages social posts, email campaigns, SMS, blog posts, contacts, and workflows.

```json
"gohighlevel": {
  "type": "stdio",
  "command": "node",
  "args": ["/path/to/GoHighLevel-MCP/dist/server.js"],
  "env": {
    "GHL_API_KEY": "your-api-key",
    "GHL_LOCATION_ID": "your-location-id"
  }
}
```

**Setup:** Clone GoHighLevel-MCP repo, build, add API key from GHL settings.

**Skills that use it:**
| Skill | GHL Tools Used |
|-------|---------------|
| `/publish social` | `create_social_post` |
| `/publish blog` | `create_blog_post` |
| `/publish sms` | `send_sms` |
| `/campaign` | `create_social_post`, `send_email`, `create_blog_post` |
| `/repurpose` | All of the above |

### 3. YouTube Transcript (Research)

Pulls transcripts from YouTube for `/research` and research.

```json
"youtube-transcript": {
  "type": "stdio",
  "command": "npx",
  "args": ["-y", "@kimtaeyoon83/mcp-server-youtube-transcript"]
}
```

### 4. Gemini (Research + Images)

Deep research, image generation, document analysis.

```json
"gemini": {
  "type": "stdio",
  "command": "env",
  "args": ["GEMINI_API_KEY=your-key", "npx", "-y", "@rlabs-inc/gemini-mcp"]
}
```

---

## OpenClaw — The Always-On Engine

OpenClaw runs on a **private server** (VPS — Hetzner, DigitalOcean, or equivalent), executing scheduled jobs against all client vaults from one machine. The client never installs or configures OpenClaw — it's part of the architect's infrastructure, shared across all clients. It connects to Telegram for delivery and approvals.

### Telegram Bot: `@Codify_build_bot`

Supergroup with 4 topic channels:

| Topic | What gets sent | Skills that feed it |
|-------|---------------|-------------------|
| **Ops** | Morning briefs, repo health, staleness alerts | `/brief` |
| **Research** | Overnight findings, positioning audits | `/research` |
| **Content** | Draft review, approval loop, posting confirmation | `/campaign`, `/repurpose` |
| **General** | Quick questions, idea capture, routing | Ad hoc |

### Scheduled Jobs

| Job | Schedule | What it does |
|-----|----------|-------------|
| Morning Brief | 5:30 AM daily | Overnight research summary, vault health, open tasks, competitor signals → Telegram Ops |
| Deep Research | 2:00 AM daily | Runs `/research` against market signals, saves to `02-Research/` |
| Content Queue | Every 5 min | Polls codify.build platform for pending content, sends to Telegram Content for approval |
| Competitor Monitor | Weekly | Tracks competitor moves, sends alerts to Telegram Research |
| Staleness Check | Daily | Flags Context files not updated in 14+ days → Telegram Ops |
| Vault Backup | Hourly | Git pull/push across all client vaults |

### How Approval Works (from Phone)

1. OpenClaw generates a draft and sends it to Telegram Content topic
2. Architect sees it on their phone
3. Reply `approve <id>` → OpenClaw publishes via GHL/Gmail
4. Reply `reject <id>` → OpenClaw archives the draft
5. Reply with feedback → OpenClaw revises and re-sends

### OpenClaw Setup Per Client

```bash
# Add a client workspace to OpenClaw
openclaw workspace create [client-name] \
  --vault-path ~/vaults/[client]-sovereign-vault \
  --telegram-topic [topic-id]

# Add morning brief cron
openclaw workspace [client-name] cron add "morning-brief" \
  --schedule "30 5 * * *"

# Add overnight research cron
openclaw workspace [client-name] cron add "deep-research" \
  --schedule "0 2 * * *"
```

### Environment Variables

```bash
# Telegram
TELEGRAM_BOT_TOKEN=your-bot-token
TELEGRAM_SUPERGROUP_ID=your-group-id
TELEGRAM_OPS_TOPIC_ID=topic-id
TELEGRAM_RESEARCH_TOPIC_ID=topic-id
TELEGRAM_CONTENT_TOPIC_ID=topic-id

# OpenRouter (model routing)
OPENROUTER_API_KEY=your-key

# Codify Platform Bridge
CODIFY_API_URL=https://codify.build
CODIFY_API_KEY=shared-secret
CODIFY_USER_ID=supabase-user-uuid
```

---

## Per-Client vs. Shared

| Connection | Shared (architect) | Per-client |
|-----------|-------------------|------------|
| GoHighLevel | One GHL account, multiple sub-accounts (locations) per client | Each client gets their own GHL Location ID |
| Gmail | Architect's Gmail for DFY sends | Client's Gmail if they want sends from their address |
| Telegram | One bot, one supergroup | Per-client topic threads within the supergroup |
| OpenClaw | One private server (VPS), all clients | Per-client workspace + cron jobs on architect's machine |
| YouTube | Shared | Shared |
| Gemini | Shared | Shared |

### Setting Up a New Client's GHL Sub-Account

1. In GoHighLevel, create a new Sub-Account (Location) for the client
2. Note the Location ID
3. When running distribution for that client, update the `GHL_LOCATION_ID` env var
4. Or maintain a lookup file mapping client → location ID

---

## How the Architect Runs Distribution

The architect does NOT run distribution from the client's Obsidian. They:

1. Pull the client's vault to their own machine (git pull)
2. Open it in their own Claude Code (with MCP servers configured)
3. Run `/publish`, `/campaign`, `/repurpose`
4. Outputs go live through the architect's MCP connections
5. Push the updated vault back (distribution logs in frontmatter)

The client sees the results in their `03-Outputs/` folder — with `published:` metadata showing where it went.

---

## Future Connections

| Platform | Status | How |
|----------|--------|-----|
| Substack | Planned | MCP server or API |
| Beehiiv | Planned | MCP server or API |
| LinkedIn direct | Planned | LinkedIn API (currently via GHL) |
| Stripe | Planned | Payment tracking in vault |
| Calendly | Planned | Booking links in campaigns |
| Slack | Available | Claude Code Slack integration |
| WhatsApp | Planned | GHL or Twilio integration |
| Podcast feed | Planned | RSS generation from vault content |
