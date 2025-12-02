---
date created: 2024-05-11, 20:09:40
date modified: 2025-11-14, 17:27:33
tags: [Interesting, Book, Studying, Productivity]
cssclasses:
  - home
---

# Books to Read

## Wishlist

| <div style="width:250px">Book<div>  | Desire | Pages | Comment            | Status   |
|-------------------------------------| ------ | ----- |:-------------------| -------- |
| [[Some book]]                       | 8      | 288   |                    | Finished |
| Another book                        | 9      | 231   | Got recommendation |          |


## Books Read

```dataviewjs
let pages = dv.pages('"Books folder"');

let data = pages.map(page => [
	page.file.name,
    page.file.link,
    ((a) => a.length > 1 ? [a[0], a.at(-1)].join(", ") : a[0])(
      page.author.replaceAll("|", "").trim().split("  ")
    ),
    page.country.replaceAll("|", "").trim().split("  ")[0],
    page.genre.replaceAll("|", "").trim(),
    page["Release date"] ? page["Release date"].replaceAll("|", "").trim().split("  ")[0] : "--",
    page["Completed reading"] ? page["Completed reading"].replaceAll("|", "").trim().split(" ")[0] : "--",
    page.pages.replaceAll("|", "").trim().split("  ")[0],
	isNaN(parseFloat(page.rating.replaceAll("|", "").trim())) ? "--" : parseFloat(page.rating.replaceAll("|", "").trim())
]);

data = data.sort();
// data = data.sort(row => row[8] == "--" ? 0 : row[8], "desc");

// ✅ Remove the first column (file name) after sorting 
data = data.map(row => row.slice(1));

dv.table(["Name", "Author", "Country", "Genre", "Release date", "Completed reading", "Pages", "Rating"], data);
```

## Key Takeaways

- [[Book 1]]
	![[Book 1#Key Takeaways]]
- [[Book 2]]
	![[Book 2#Key Takeaways]]
