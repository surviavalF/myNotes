---
banner: "https://api.dujin.org/bing/1366.php"
banner_x: 0.5
---


```dataviewjs
let ftMd = dv.pages("").file.sort(t => t.cday)[0]
let total = parseInt([new Date() - ftMd.ctime] / (60*60*24*1000))
let totalDays = " 您已使用 *Obsidian* "+total+" 天，"
let nofold = '!"misc/templates"'
let allFile = dv.pages(nofold).file
let totalMd = "共创建 "+
	allFile.length+" 篇笔记"
let totalTag = allFile.etags.distinct().length+" 个标签"

dv.paragraph(
	totalDays+totalMd+"、"+totalTag+""
)
```

----


```dataviewjs
	let pages = dv.pages('"开发笔记"');
	dv.table(
		["名字","创建时间"],
		pages.sort(b => b.file.cday,"desc")
			.map(b => [b.file.link,b.file.cday])
	)
```
