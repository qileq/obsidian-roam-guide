
```dataview
Table
	WITHOUT ID
	file.name AS 书名,
	embed(link(cover)) AS 封面, 
	author AS 作者, 
	rating AS 评分, 
	status AS 进度
FROM #book 
SORT status DESC
```
