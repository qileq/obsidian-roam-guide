## Dateview
```dataview
Table
	embed(link(cover)) AS 封面,
	author AS 作者, 
	rating AS 评分, 
	choice(lower(status)="todo", "🔴", choice(lower(status)="in progress", "🟡", "🟢")) AS 状态
FROM #book AND -"templates"
SORT status DESC
```

可以使用 `coverLink AS 封面` 代替 `embed(link(cover)) AS 封面` 展示图片。

## DataviewJS
### Table
```dataviewjs
dv.table(["书名", "封面", "作者", "评分", "进度"], dv.pages('#book AND -"templates"')
  .sort(b => b.status, 'desc')
  .map(b => [b.file.link, dv.fileLink(b.cover, true), b.author, b.rating, b.status.toLowerCase()=="todo" ? "🔴" : (b.status.toLowerCase()=="done" ? "🟢" : "🟡")]))
```


### 分组
```dataviewjs
for (let group of dv.pages('#book AND -"templates"').groupBy(p => p.status)) {     
  dv.header(3, group.key); 
  dv.table(["书名", "封面", "作者", "评分"], 
	group.rows
		.sort(b => b.rating, 'desc') 
		.map(b => [b.file.link, dv.fileLink(b.cover, true), b.author, b.rating])
  ) 
}
```


### 结合 Admonition 展示

````ad-info
title: 阅读清单
icon: book
collapse: open
color: 0, 169, 206

```dataviewjs
dv.header(3, "📚 Books"); 
dv.table(["书名", "封面", "作者", "评分", "进度"], dv.pages('#book AND -"templates"')
  .sort(b => b.status, 'desc')
  .map(b => [b.file.link, dv.fileLink(b.cover, true), b.author, b.rating, b.status]))
```
````
