---
name: brief
description: "Morning brief — overnight research, vault health, open tasks, and recommended focus for the day."
---

# /brief — Morning Brief

Generates a daily executive summary from your vault. What changed overnight, what needs attention, and where to focus today.

## Usage

```
/brief              → Today's morning brief
/brief weekly       → Week-in-review summary
```

## Procedure

### 1. Scan Vault Activity

Check for changes since last brief:
- New files in `01-Decisions/`, `02-Research/`
- Modified Soul files
- New outputs generated
- Recent git commits (via `git log --since="24 hours ago"`)

### 2. Check Vault Health

Run a silent `/audit`:
- Context Power score
- Stale files count
- Orphaned notes count
- Biggest enrichment opportunity

### 3. Check Open Tasks

Scan for unchecked tasks across the vault:
```
- [ ] incomplete tasks in any markdown file
```

### 4. Generate Brief

Format:

```markdown
# Morning Brief — [date]

## Overnight Activity
- [what changed since yesterday]

## Vault Health
- Context Power: [score]
- Stale files: [count]
- Biggest gap: [specific suggestion]

## Open Tasks
- [ ] [task 1]
- [ ] [task 2]

## Recommended Focus
[1-2 sentence recommendation based on vault state and recent activity]
```

### 5. Save + Display

Save to `04-Daily/[date]-brief.md` and display in terminal.
