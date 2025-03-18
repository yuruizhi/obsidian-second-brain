# Dataview 查询示例

## 项目一览查询

```dataview
TABLE
file.ctime as "创建时间",
file.mtime as "最后修改"
FROM "1-项目"
WHERE contains(file.name, "项目简介")
SORT file.mtime DESC
```


## 最近修改的资源

```dataview
TABLE file.mtime as "最后修改"
FROM "3-资源"
SORT file.mtime DESC
LIMIT 10
```

## 带特定标签的笔记

```dataview
LIST
FROM #需要回顾
SORT file.mtime DESC
```


## 未完成任务追踪

```dataview
TASK
FROM "1-项目" or "2-领域"
WHERE !completed
GROUP BY file.link
```


## 按创建日期列出笔记

```dataview
TABLE
dateformat(file.ctime, "yyyy-MM-dd") as "创建日期"
FROM "0-收集箱" or "1-项目" or "3-资源"
SORT file.ctime DESC
LIMIT 15
```


## 相关笔记查询(从当前笔记)

```dataview
LIST
FROM [[]]
```

## 高级：YAML属性查询
```dataview
TABLE
authors as "作者",
dateformat(file.ctime, "yyyy-MM-dd") as "创建日期"
FROM "3-资源/书籍笔记"
WHERE authors
SORT authors ASC
```

## 提示
- 这些查询可以复制到其他笔记中
- 可以根据需要调整查询条件
- 使用 ```dataview 语法创建查询
- 查询结果会随着笔记库变化而动态更新