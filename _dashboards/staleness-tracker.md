---
type: dashboard
---

# What Needs Attention

Files that need a refresh. Stale context = stale outputs.

---

## Context Files — Last Updated

```dataview
TABLE
  dateformat(file.mtime, "yyyy-MM-dd") as "Last Updated",
  choice(date(now) - file.mtime > dur(30 days), "🔴 Overdue", choice(date(now) - file.mtime > dur(14 days), "🟡 Review soon", "🟢 Current")) as "Status"
FROM "00-Context"
SORT file.mtime ASC
```

---

## Unconnected Files

Files not linked to anything else in your vault:

```dataview
LIST
FROM "00-Context" OR "01-Decisions" OR "02-Research"
WHERE length(file.outlinks) = 0
```

---

## Open Tasks

```dataview
TASK
FROM "01-Decisions" OR "02-Research"
WHERE !completed
```
