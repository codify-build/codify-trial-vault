---
type: dashboard
---

# What Needs Attention

Files that need a refresh. Stale context = stale outputs.

---

## Context Files — Last Updated

```dataview
TABLE
  last-updated as "Last Updated",
  choice(status = "compounding", "Deep", choice(status = "active", "Solid", choice(status = "draft", "Getting there", "Empty"))) as "Depth",
  choice(date(now) - file.mtime > dur(30 days), "Overdue", choice(date(now) - file.mtime > dur(14 days), "Review soon", "Current")) as "Freshness"
FROM "00-Context"
SORT file.mtime ASC
```

---

## Unconnected Files

Files not linked to anything else in your vault:

```dataview
LIST
FROM "00-Context" OR "01-Decisions" OR "02-Research"
WHERE length(file.outlinks) = 0 AND length(file.inlinks) = 0
```

---

## Open Tasks

```dataview
TASK
FROM "01-Decisions" OR "02-Research"
WHERE !completed
```
