---
type: dashboard
---

# Context Power

Your business brain at a glance. The more complete your Context files, the better your outputs.

---

## Your Context Files

```dataview
TABLE
  choice(status = "compounding", "Deep", choice(status = "active", "Solid", choice(status = "draft", "Getting there", "Empty"))) as "Depth",
  choice(length(file.outlinks) > 2, "Connected", choice(length(file.outlinks) > 0, "Some links", "No links yet")) as "Connections",
  last-updated as "Last Updated"
FROM "00-Context"
SORT file.name ASC
```

### What to do next
- **Empty** — Run `/extract` to fill it in
- **Getting there** — Run `/enrich` to go deeper
- **Solid** — Enriched but needs cross-references to other files
- **Deep** — Rich, linked, compounding. This is your competitive edge.

---

## Recent Decisions

```dataview
TABLE
  last-updated as "Last Updated",
  status as "Status"
FROM "01-Decisions"
SORT date DESC
LIMIT 5
```

---

## Recent Outputs

```dataview
TABLE
  format as "Type",
  last-updated as "Last Updated"
FROM "03-Outputs"
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
