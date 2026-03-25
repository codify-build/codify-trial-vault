---
type: dashboard
---

# Context Power Dashboard

Your reference stack at a glance. The more complete your Soul files, the better your AI outputs.

---

## Soul File Health

```dataview
TABLE
  choice(length(file.outlinks) > 2, "🔗 Connected", "⚠️ Isolated") as "Links",
  choice(file.size > 500, "✅ Rich", choice(file.size > 200, "📝 Draft", "🔲 Empty")) as "Depth",
  dateformat(file.mtime, "yyyy-MM-dd") as "Last Updated",
  choice(date(now) - file.mtime > dur(14 days), "🔴 Stale", "🟢 Fresh") as "Freshness"
FROM "00-Soul"
SORT file.name ASC
```

---

## Recent Decisions

```dataview
TABLE
  dateformat(date, "yyyy-MM-dd") as "Date",
  status as "Status",
  length(file.outlinks) as "Cross-Refs"
FROM "01-Decisions"
SORT date DESC
LIMIT 10
```

---

## Recent Research

```dataview
TABLE
  dateformat(date, "yyyy-MM-dd") as "Date",
  length(file.outlinks) as "Cross-Refs"
FROM "02-Research"
SORT date DESC
LIMIT 10
```

---

## Staleness Alert

Files not updated in 14+ days:

```dataview
LIST
FROM "00-Soul" OR "01-Decisions"
WHERE date(now) - file.mtime > dur(14 days)
SORT file.mtime ASC
```

---

## Your Compound Score

| Metric | Count |
|--------|-------|
| Soul files | `$= dv.pages('"00-Soul"').length` |
| Decisions logged | `$= dv.pages('"01-Decisions"').length` |
| Research files | `$= dv.pages('"02-Research"').length` |
| Outputs generated | `$= dv.pages('"03-Outputs"').length` |
| Daily notes | `$= dv.pages('"04-Daily"').length` |
| **Total vault files** | `$= dv.pages().length` |

> The more files, the more cross-references. The more cross-references, the better your AI understands your business. That's the compound loop.
