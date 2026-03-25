---
name: update
description: "Pull the latest skills, dashboards, and architecture from Codify without touching client data."
---

# /update — Update Your Business Brain

Pulls the latest Codify skills, dashboards, and system files from the template repo. Never touches client data (Soul files, decisions, research, outputs, daily notes).

## What Gets Updated

| Updated (from Codify) | Never Touched (yours) |
|-----------------------|----------------------|
| `.claude/skills/` | `00-Soul/` |
| `_dashboards/` | `01-Decisions/` |
| `_templates/` | `02-Research/` |
| `CLAUDE.md` | `03-Outputs/` |
| `.obsidian/plugins/` | `04-Daily/` |

## Procedure

### 1. Check for Upstream Remote

```bash
# Check if upstream remote exists
git remote -v | grep upstream
```

If upstream is missing, add it silently:

```bash
git remote add upstream https://github.com/mike-scott-darwin/codify-vault-template.git
```

### 2. Fetch Latest Updates

```bash
git fetch upstream main --quiet
```

### 3. Pull Only System Files

Do NOT merge the full branch. Cherry-pick only the system directories:

```bash
# Update skills
git checkout upstream/main -- .claude/skills/

# Update dashboards
git checkout upstream/main -- _dashboards/

# Update templates
git checkout upstream/main -- _templates/ 2>/dev/null || true

# Update system config
git checkout upstream/main -- CLAUDE.md

# Update plugin configs (not plugin binaries — those are large)
git checkout upstream/main -- .obsidian/community-plugins.json
git checkout upstream/main -- .obsidian/plugins/agent-client/data.json 2>/dev/null || true
```

### 4. Commit the Update

```bash
git add -A
git commit -m "[update] Codify system update — $(date +%Y-%m-%d)" --allow-empty
git push origin main --quiet
```

### 5. Report

Say:
"Your system is up to date. Here's what changed:"

Then list any new or modified skills. If nothing changed:

"You're already on the latest version. Nothing to update."

## Auto-Update on Startup

This skill can be triggered automatically. When Claude Code starts in a vault, check the last update date:

```bash
# Check last update timestamp
LAST_UPDATE=$(git log --oneline --grep="Codify system update" -1 --format="%cd" --date=short 2>/dev/null)
TODAY=$(date +%Y-%m-%d)

if [ "$LAST_UPDATE" != "$TODAY" ]; then
    # Run update silently
    git fetch upstream main --quiet 2>/dev/null
    git checkout upstream/main -- .claude/skills/ 2>/dev/null
    git checkout upstream/main -- _dashboards/ 2>/dev/null
    git checkout upstream/main -- CLAUDE.md 2>/dev/null
    git add -A
    git diff --cached --quiet || git commit -m "[update] Codify system update — $TODAY" --quiet
fi
```

## Tone

- **Invisible.** The client should barely notice this happening.
- **Quick.** This should take under 5 seconds.
- **Safe.** Never touch Soul files, decisions, research, outputs, or daily notes.

## Error Handling

| Situation | What to do |
|-----------|-----------|
| No internet | Skip silently. Say nothing. Try again next time. |
| Merge conflict in CLAUDE.md | Keep the client's version. System files should never conflict with client data. |
| Upstream repo not accessible | Skip silently. The vault works fine without updates. |
| Client asks what happened | "I checked for system updates. Your files are untouched — I only update the tools." |
