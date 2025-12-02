---
date created: 2025-05-11, 20:09:40
date modified: 2025-11-07, 16:57:02
tags:
  - Interesting
  - Game
cssclasses:
  - home
---

# Games to Play

## Wishlist

### AAAAAAAA Games

| <div style="width:250px">Game<div> | Desire | Time to beat | Requirement      | Comment                                       | Status   |
|------------------------------------|--------| ------------ |------------------|-----------------------------------------------| -------- |
| [[Some game]]                      | 10     | 130          | Waiting for DLC  | Plus giving myself a brake from this category | Finished |
| Another game                       | 8      | 40           |                  |                                               |          |

### Indie Games

| <div style="width:250px">Game<div> | Desire | Time to beat | Requirement  | Comment          | Status   |
|------------------------------------| ------ | ------------ |--------------|------------------| -------- |
| [[Some game]]                      | 9      | 6            |              |                  | Finished |
| Another game                       | 8      | 3            |              | 3D cube puzzle   |          |


### Coop Games

| <div style="width:250px">Game<div> | Desire | Time to beat | Requirement         | Comment             | Status   |
|------------------------------------|--------| ------------ | ------------------- |---------------------| -------- |
| [[Some Game]]                      | 9      | 6            |                     | Split screen Coop   | Finished |
| Another game                       | 7      | -            | Waiting for release |                     |          |

## Games Played

```dataviewjs
let pages = dv.pages('"Games folder"');

let data = pages.map(page => [
	page.file.name,
    page.file.link,
    page.developer.replaceAll("|", "").trim().split("  ")[0],
    page.country.replaceAll("|", "").trim().split("  ")[0],
    page.publisher.replaceAll("|", "").trim().split("  ")[0],
    page.genre.replaceAll("|", "").trim().split("  ")[0],
    page["Release date"] ? page["Release date"].replaceAll("|", "").trim().split(" ")[0] : "--",
    isNaN(parseFloat(page["Time spent"].replaceAll("|", "").trim())) ? 0 : parseFloat(page["Time spent"].replaceAll("|", "").trim()),
	isNaN(parseFloat(page.rating.replaceAll("|", "").trim())) ? "--" : parseFloat(page.rating.replaceAll("|", "").trim())
]);

data = data.sort();
// data = data.sort(row => row[8] == "--" ? 0 : row[8], "desc");

// ✅ Remove the first column (file name) after sorting 
data = data.map(row => row.slice(1));

let total = 0.0;
data.forEach(row => {
    total += row[6];
});

data["values"][data.length] = ["###"]

data["values"][data.length + 1] = [
    "***Total***",
    "",
    "",
    "",
    "",
    "",
    total,
    ""
];

dv.table(["Name", "Developer", "Country", "Publisher", "Genre", "Release date", "Time spent", "Rating"], data);
```

## Key Takeaways

- [[Game 1]]
	![[Game 1#Key Takeaways]]
- [[Game 2]]
	![[Game 2#Key Takeaways]]
