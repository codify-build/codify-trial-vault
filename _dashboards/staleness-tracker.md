---
type: dashboard
---

# Staleness Tracker

Files that need your attention. Stale context = stale AI outputs.

---

## Context Files — Last Updated

```dataview
TABLE
  dateformat(file.mtime, "yyyy-MM-dd") as "Last Updated",
  choice(date(now) - file.mtime > dur(30 days), "🔴 Overdue", choice(date(now) - file.mtime > dur(14 days), "🟡 Review Soon", "🟢 Current")) as "Status"
FROM "00-Context"
SORT file.mtime ASC
```

---

## Orphaned Files

Files with no outgoing links (not connected to your knowledge graph):

```dataview
LIST
FROM "00-Context" OR "01-Decisions" OR "02-Research"
WHERE length(file.outlinks) = 0
```

---

## Action Items

Open tasks across your vault:

```dataview
TASK
FROM "01-Decisions" OR "02-Research"
WHERE !completed
```
