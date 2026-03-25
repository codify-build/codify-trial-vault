---
type: dashboard
---

# Context Power

Your business brain at a glance. The more complete your Context files, the better your outputs.

---

## Your Context Files

```dataview
TABLE
  choice(length(file.outlinks) > 2, "🔗 Connected", "⚠️ Needs links") as "Connections",
  choice(file.size > 500, "✅ Strong", choice(file.size > 200, "📝 Getting there", "🔲 Empty")) as "Strength",
  dateformat(file.mtime, "yyyy-MM-dd") as "Last Updated",
  choice(date(now) - file.mtime > dur(14 days), "🔴 Needs refresh", "🟢 Current") as "Freshness"
FROM "00-Context"
SORT file.name ASC
```

---

## Recent Decisions

```dataview
TABLE
  dateformat(date, "yyyy-MM-dd") as "Date",
  status as "Status"
FROM "01-Decisions"
SORT date DESC
LIMIT 5
```

---

## Recent Research

```dataview
TABLE
  dateformat(date, "yyyy-MM-dd") as "Date"
FROM "02-Research"
SORT date DESC
LIMIT 5
```

---

## Needs Attention

Files not updated in 14+ days:

```dataview
LIST
FROM "00-Context" OR "01-Decisions"
WHERE date(now) - file.mtime > dur(14 days)
SORT file.mtime ASC
```

---

## Your Vault at a Glance

| What | Count |
|------|-------|
| Context files | `$= dv.pages('"00-Context"').length` |
| Decisions | `$= dv.pages('"01-Decisions"').length` |
| Research | `$= dv.pages('"02-Research"').length` |
| Outputs | `$= dv.pages('"03-Outputs"').length` |
| Daily notes | `$= dv.pages('"04-Daily"').length` |

> More files = more connections. More connections = better outputs. That's how your vault gets smarter over time.
