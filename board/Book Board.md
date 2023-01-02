## Dateview
```dataview
Table
	WITHOUT ID
	file.name AS 书名,
	embed(link(cover)) AS 封面, 
	author AS 作者, 
	rating AS 评分, 
	status AS 进度
FROM #book AND -"templates"
SORT status DESC
```



## DataviewJS
### Table
```dataviewjs
dv.table(["书名", "封面", "作者", "评分", "进度"], dv.pages('#book AND -"templates"')
  .sort(b => b.status, 'desc')
  .map(b => [b.file.name, dv.fileLink(b.cover, true), b.author, b.rating, b.status]))
```

### 分组
```dataviewjs
for (let group of dv.pages('#book AND -"templates"').groupBy(p => p.status)) {     
  dv.header(3, group.key); 
  dv.table(["书名", "封面", "作者", "评分"], 
	group.rows
		.sort(b => b.rating, 'desc') 
		.map(b => [b.file.name, dv.fileLink(b.cover, true), b.author, b.rating])
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
  .map(b => [b.file.name, dv.fileLink(b.cover, true), b.author, b.rating, b.status]))
```
````
