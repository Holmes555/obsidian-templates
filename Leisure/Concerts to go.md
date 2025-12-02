---
date created: 2025-03-02, 19:09:40
date modified: 2025-11-12, 19:41:29
tags: [Concert, Music, Interesting]
cssclasses:
  - home
---

# Concerts to Go

## Wishlist

| <div style="width:250px">Concert<div> | Desire | Location        | <div style="width:85px">Date<div> | <div style="width:65px">Cost<div> | Place | Comment               | Status |
|---------------------------------------| ------ |-----------------| --------------------------------- |-----------------------------------| ----- |:----------------------| ------ |
| [[Some concert]]                      | 8      | Berlin, Germany | 06-03-2025                        | 100 EUR                           | GA    | Already bought ticket | Went   |
| Another concert                       | 10     | Paris, France   | 09-02-2026                        | 85 EUR                            | GA    | Already bought ticket |        |

## Films Watched

```dataviewjs
let pages = dv.pages('"Concerts folder"');

let data = pages.map(page => [
	page.file.name,
    page.file.link,
    page.language.replaceAll("|", "").trim().split("  ")[0],
    page.country.replaceAll("|", "").trim().split("  ")[0],
    page.genre.replaceAll("|", "").trim().split("  ")[0],
    page["Years active"] ? page["Years active"].replaceAll("|", "").trim().split("  ")[0] : "--",
    page["Concert date"] ? page["Concert date"].replaceAll("|", "").trim().split(" ")
    .filter(r => r !== "").join("; ") : "--",
    page["Concert location"] ? page["Concert location"].replaceAll("|", "").trim().split(" ")
    .filter(r => r !== "")
    .reduce((acc, curr, index, arr) => {
        if (index % 2 === 0) acc.push(curr + " " + (arr[index + 1] || ""));
        return acc;
    }, []).join("; ") : "--",
	page.rating.replaceAll("|", "").trim().split(" ").filter(r => r !== "").join("; "),
]);

data = data.sort();
// data = data.sort(row => row[8] == "--" ? 0 : row[8], "desc");

// ✅ Remove the first column (file name) after sorting 
data = data.map(row => row.slice(1));

dv.table(["Name", "Language", "Country", "Genre", "Years active", "Concert date", "Concert location", "Rating"], data);
```

## Key Takeaways

- [[Concert 1]]
	![[Concert 1#Key Takeaways]]
- [[Concert 2]]
	![[Concert 2#Key Takeaways]]
