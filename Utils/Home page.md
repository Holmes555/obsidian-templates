---
date created: 2025-04-21, 15:48:40
date modified: 2025-12-07, 19:14:29
tags:
  - Productivity
cssclasses:
  - home
---

# Home Page

Start your journey here!

```ad-tip
Recall old ideas with opening a random note.
```

```dataviewjs
const today = new Date();
const thisWeekStart = new Date(today);
thisWeekStart.setDate(today.getDate() - (today.getDay() === 0 ? 6 : today.getDay() - 1)); // Start of the week (Monday)
thisWeekStart.setHours(0, 0, 0, 0);
const thisMonthStart = new Date(today.getFullYear(), today.getMonth(), 1); // Start of the current month
thisMonthStart.setHours(0, 0, 0, 0);
const thisYear = new Date(new Date().getFullYear(), 0, 1);
thisYear.setHours(0, 0, 0, 0);

const filteredPages = dv.pages()
    .filter(p => !p.file.folder.startsWith("Some filter out folder"))
    .filter(p => !p.file.folder.startsWith("Another filter out folder"));

// Files created this week
const createdFilesThisWeekStart = filteredPages.filter(p => new Date(p["date created"]) >= thisWeekStart);
const totalCreatedFilesThisWeekStart = createdFilesThisWeekStart.length;

// Files updated this week
const updatedFilesThisWeekStart = filteredPages.filter(p => new Date(p["date modified"]) >= thisWeekStart);
const totalUpdatedFilesThisWeekStart = updatedFilesThisWeekStart.length;

// Files created this month
const createdFilesThisMonth = filteredPages.filter(p => new Date(p["date created"]) >= thisMonthStart);
const totalCreatedFilesThisMonth = createdFilesThisMonth.length;

// Files updated this month
const updatedFilesThisMonth = filteredPages.filter(p => new Date(p["date modified"]) >= thisMonthStart);
const totalUpdatedFilesThisMonth = updatedFilesThisMonth.length;

// Files created this year
const createdFiles = filteredPages.filter(p => new Date(p["date created"]) >= thisYear);
const totalCreatedFiles = createdFiles.length;

// Files updated this year
const updatedFiles = filteredPages.filter(p => new Date(p["date modified"]) >= thisYear);
const totalUpdatedFiles = updatedFiles.length;

// Total files
const totalFiles = filteredPages.length;

// Display results
dv.paragraph(`**Total Files Created This Week:** ${totalCreatedFilesThisWeekStart}`);
dv.paragraph(`**Total Files Updated This Week:** ${totalUpdatedFilesThisWeekStart}`);
dv.paragraph(`**Total Files Created This Month:** ${totalCreatedFilesThisMonth}`);
dv.paragraph(`**Total Files Updated This Month:** ${totalUpdatedFilesThisMonth}`);
dv.paragraph(`**Total Files Created This Year:** ${totalCreatedFiles}`);
dv.paragraph(`**Total Files Updated This Year:** ${totalUpdatedFiles}`);
dv.paragraph(`**Total Files:** ${totalFiles}`);
```

```dataviewjs
const files = dv.pages()
    .filter(p => !p.file.folder.startsWith("Some filter out folder"))
    .filter(p => !p.file.folder.startsWith("Another filter out folder")); // Get all pages

// Validate and parse dates safely
function safeDate(dateString) {
    const parsedDate = new Date(dateString);
    return isNaN(parsedDate) ? null : parsedDate;
}

// Helper to generate full range of months between two dates
function getMonthlyRange(start, end) {
    const range = [];
    let current = new Date(start.getFullYear(), start.getMonth(), 1);
    const last = new Date(end.getFullYear(), end.getMonth(), 1);

    while (current <= last) {
        range.push(`${current.getFullYear()}-${String(current.getMonth() + 1).padStart(2, '0')}`);
        current.setMonth(current.getMonth() + 1);
    }
    return range;
}

// Helper to generate full range of weeks between two dates
function getWeeklyRange(start, end) {
    const range = [];
    let current = new Date(start);
    current.setDate(current.getDate() - (current.getDay() === 0 ? 6 : current.getDay() - 1)); // Start on Monday
    current.setHours(0, 0, 0, 0);

    const last = new Date(end);
    last.setDate(last.getDate() - (last.getDay() === 0 ? 6 : last.getDay() - 1));
    last.setHours(0, 0, 0, 0);

    while (current <= last) {
        range.push(current.toISOString().split('T')[0]); // Use ISO string for consistency
        current.setDate(current.getDate() + 7); // Increment by 7 days
    }
    return range;
}

// Group by Month
const monthlyCreatedCounts = {};
const monthlyUpdatedCounts = {};
files.forEach(p => {
    const createdDate = safeDate(p["date created"]);
    if (createdDate) {
        const monthKey = `${createdDate.getFullYear()}-${String(createdDate.getMonth() + 1).padStart(2, '0')}`; // e.g., "2024-12"
        monthlyCreatedCounts[monthKey] = (monthlyCreatedCounts[monthKey] || 0) + 1;
    }
    const updatedDate = safeDate(p["date modified"]);
    if (updatedDate) {
        const monthKey = `${updatedDate.getFullYear()}-${String(updatedDate.getMonth() + 1).padStart(2, '0')}`; // e.g., "2024-12"
        monthlyUpdatedCounts[monthKey] = (monthlyUpdatedCounts[monthKey] || 0) + 1;
    }
    
});

// Group by Week
const weeklyCreatedCounts = {};
const weeklyUpdatedCounts = {};
files.forEach(p => {
    const createdDate = safeDate(p["date created"]);
    if (createdDate) {
        const weekStart = new Date(createdDate);
        weekStart.setDate(createdDate.getDate() - (createdDate.getDay() === 0 ? 6 : createdDate.getDay() - 1)); // Calculate Monday
        weekStart.setHours(0, 0, 0, 0); // Reset time to midnight
        const weekKey = weekStart.toISOString().split('T')[0]; // Use date string as key
        weeklyCreatedCounts[weekKey] = (weeklyCreatedCounts[weekKey] || 0) + 1;
    }
    const updatedDate = safeDate(p["date modified"]);
    if (updatedDate) {
        const weekStart = new Date(updatedDate);
        weekStart.setDate(updatedDate.getDate() - (updatedDate.getDay() === 0 ? 6 : updatedDate.getDay() - 1)); // Calculate Monday
        weekStart.setHours(0, 0, 0, 0); // Reset time to midnight
        const weekKey = weekStart.toISOString().split('T')[0]; // Use date string as key
        weeklyUpdatedCounts[weekKey] = (weeklyUpdatedCounts[weekKey] || 0) + 1;
    }
});

// Get earliest and latest dates from files
const allDates = files.map(p => safeDate(p["date created"])).filter(Boolean);
const earliestDate = new Date(Math.min(...allDates));
const latestDate = new Date(Math.max(...allDates));

// Generate Data for Graphs
const monthlyLabels = getMonthlyRange(earliestDate, latestDate);
const monthlyCreatedData = monthlyLabels.map(key => monthlyCreatedCounts[key] || 0);
const monthlyUpdatedData = monthlyLabels.map(key => monthlyUpdatedCounts[key] || 0);

const weeklyLabels = getWeeklyRange(earliestDate, latestDate);
const weeklyCreatedData = weeklyLabels.map(key => weeklyCreatedCounts[key] || 0);
const weeklyUpdatedData = weeklyLabels.map(key => weeklyUpdatedCounts[key] || 0);


// Render the Monthly Bar Chart using the Charts plugin
dv.paragraph(`
~~~chart
	type: bar
	labels: [${monthlyLabels.map(label => `"${label}"`).join(", ")}]
	series: 
	  - label: "Monthly Created File Count"
		data: [${monthlyCreatedData.join(", ")}]
		backgroundColor: rgba(255, 99, 132, 0.2)
		borderColor: rgba(255, 99, 132, 1)
		borderWidth: 1
	  - label: "Monthly Updated File Count"
		data: [${monthlyUpdatedData.join(", ")}]
		backgroundColor: rgba(54, 162, 235, 0.2)
        borderColor: rgba(54, 162, 235, 1)
		borderWidth: 1
~~~
`);

// Render the Weekly Bar Chart using the Charts plugin
dv.paragraph(`
~~~chart
	type: line
	labels: [${weeklyLabels.map(label => `"${label}"`).join(", ")}]
	series: 
	  - label: "Weekly Created File Count"
		data: [${weeklyCreatedData.join(", ")}]
		backgroundColor: rgba(246, 217, 29, 0.2)
		borderColor: rgba(246, 217, 29, 1)
		borderWidth: 1
	  - label: "Weekly Updated File Count"
		data: [${weeklyUpdatedData.join(", ")}]
		backgroundColor: rgba(30, 236, 112, 0.2)
		borderColor: rgba(30, 236, 112, 1)
		borderWidth: 1
~~~
`);
```

<font color="#92d050">TODO In Progress</font>
![[TODO list#In Progress]]

<font color="#ffc000">Backlog Active</font>
![[Backlog#Active]]
