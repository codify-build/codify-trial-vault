---
type: dashboard
---

# Reference Health

How deep is your context? Deeper files = better outputs.

---

## Context File Strength

```dataview
TABLE
  choice(file.size > 1000, "🟢 Deep", choice(file.size > 500, "🟡 Solid", choice(file.size > 200, "🟠 Getting there", "🔴 Empty"))) as "Strength",
  length(file.outlinks) as "Links to other files",
  length(file.inlinks) as "Referenced by"
FROM "00-Context"
SORT file.size DESC
```

### What the levels mean
- **Empty** — Template only. Run `/extract` to fill it in.
- **Getting there** — Some answers. Run `/enrich` to go deeper.
- **Solid** — Good content. Connected to other files. AI can use this well.
- **Deep** — Rich, linked, actively maintained. This is your competitive edge.

---

## Most Connected Files

Your best-linked files — these make your outputs strongest:

```dataview
TABLE
  length(file.outlinks) + length(file.inlinks) as "Total Connections"
FROM ""
SORT (length(file.outlinks) + length(file.inlinks)) DESC
LIMIT 10
```

---

## Ready to Generate?

When your Context files reach "Solid" strength, your outputs will be sharp and specific. Until then, keep enriching with `/enrich` or import more material with `/import`.
