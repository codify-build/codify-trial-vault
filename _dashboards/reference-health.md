---
type: dashboard
---

# Reference Health

How deep is your context? Deeper files = better AI outputs.

---

## File Depth by Folder

### Soul Files (Core Identity)
```dataview
TABLE
  file.size as "Size (bytes)",
  choice(file.size > 1000, "Compounding", choice(file.size > 500, "Working", choice(file.size > 200, "Draft", "Skeleton"))) as "Depth Level",
  length(file.outlinks) as "Outlinks",
  length(file.inlinks) as "Inlinks"
FROM "00-Soul"
SORT file.size DESC
```

### Depth Levels
- **Skeleton** — Template only. No real content yet.
- **Draft** — Some answers filled in. Needs enrichment.
- **Working** — Solid content. Cross-referenced. Usable by AI.
- **Compounding** — Deep, linked, actively maintained. Your moat.

---

## Cross-Reference Density

Most connected files in your vault:

```dataview
TABLE
  length(file.outlinks) + length(file.inlinks) as "Total Connections",
  length(file.outlinks) as "Links Out",
  length(file.inlinks) as "Links In"
FROM ""
SORT (length(file.outlinks) + length(file.inlinks)) DESC
LIMIT 15
```

---

## Content Generation Readiness

```dataview
TABLE WITHOUT ID
  "Soul files at Working+ depth" as "Metric",
  length(filter(dv.pages('"00-Soul"'), (p) => p.file.size > 500)) as "Count"
```

> When all 4 Soul files hit "Working" depth, you're ready to generate high-fidelity outputs. Until then, keep enriching.
