---
date created: 2024-04-17, 00:00:00
date modified: 2024-12-05, 21:15:04
---

# TODO List

## In Progress

```dataview
TABLE WITHOUT ID
file.link AS Name,
choice(status, "✅", "❌") as Status,
date(split(row["date created"], ",")[0]) AS "Created At",
file.folder AS Path, 
file.etags AS Tags
FROM #TODO 
WHERE file.folder != "Filter out folder" 
AND file.name != "Filter out filename" 
AND !status
SORT date(split(row["date created"], ",")[0]) DESC
```

## Completed

```dataview
TABLE WITHOUT ID
file.link AS Name,
choice(status, "✅", "❌") as Status,
date(split(row["date created"], ",")[0]) AS "Created At",
file.folder AS Path, 
file.etags AS Tags
FROM #TODO 
WHERE file.folder != "Filter out folder" 
AND file.name != "Filter out filename" 
AND status
SORT date(split(row["date created"], ",")[0]) DESC
```
