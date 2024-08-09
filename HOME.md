---
banner: "https://api.dujin.org/bing/1366.php"
banner_x: 0.5
---
## 欢迎回来

```dataviewjs
let ftMd = dv.pages("").file.sort(t => t.cday)[0]
let total = parseInt([new Date() - ftMd.ctime] / (60*60*24*1000))
let totalDays = " 您已坚持记笔记 "+total+" 天，"
let nofold = '!"misc/templates"'
let allFile = dv.pages(nofold).file
let totalMd = "共创建 "+
	allFile.length+" 篇笔记"

function formatNumberWithSpaces(number) { 
	return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " "); 
}
let totalWordCount = 0; 
for (let file of app.vault.getMarkdownFiles()) { 
	let content = await app.vault.read(file); 
	let wordCount = content.split(/\s+/).filter(word => word.trim().length > 0).length; 
	totalWordCount += wordCount; 
}

let formattedTotal = "总字数 "+ formatNumberWithSpaces(totalWordCount) + " 字";

dv.paragraph(
	totalDays+totalMd+"、"+formattedTotal+""
)
```

----

## 每日金句
```dataviewjs

```
```dataviewjs
let file = app.vault.getAbstractFileByPath("读书笔记/摘抄.md"); 
let content = await app.vault.read(file); 
let quotes = content.split(/```/).filter(quote => quote.trim() !=="").map(quote => quote.trim()); let randomQuote = quotes[Math.floor(Math.random() * quotes.length)]; dv.paragraph(randomQuote);
```

----
