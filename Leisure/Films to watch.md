---
date created: 2025-05-11, 20:09:40
date modified: 2025-09-26, 22:38:02
tags:
  - Wastetime
  - Film
cssclasses:
  - home
---

# Films to Watch

## Wishlist

| <div style="width:250px">Book<div>     | Desire | Comment | Status  |
|----------------------------------------|--------|:--------| ------- |
| [[Some film]]                          | 8      |         | Watched |
| Another film                           | 6      | Series  |         |

## Films Watched

```dataviewjs
let pages = dv.pages('"Films folder"');

let data = pages.map(page => [
	page.file.name,
    page.file.link,
    page.director.replaceAll("|", "").trim().split("  ")[0],
    page.country.replaceAll("|", "").trim().split("  ")[0],
    page.genre.replaceAll("|", "").trim().split("  ")[0],
    page["Release date"] ? page["Release date"].replaceAll("|", "").trim().split("  ")[0] : "--",
    page.duration.replaceAll("|", "").trim().split("  ")[0],
    page.status.replaceAll("|", "").trim().split("  ")[0],
	isNaN(parseFloat(page.rating.replaceAll("|", "").trim())) ? "--" : parseFloat(page.rating.replaceAll("|", "").trim())
]);

data = data.sort();
// data = data.sort(row => row[8] == "--" ? 0 : row[8], "desc");

// ✅ Remove the first column (file name) after sorting 
data = data.map(row => row.slice(1));

dv.table(["Name", "Director", "Country", "Genre", "Release date", "Duration", "Status", "Rating"], data);
```

## Key Takeaways

- [[Film 1]]
	![[Film 1#Key Takeaways]]
- [[Film 2]]
	![[Film 2#Key Takeaways]]
