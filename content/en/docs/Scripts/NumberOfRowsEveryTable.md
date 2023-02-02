---
title: "Find the number of rows in every table in your database"
description: "Search all objects in SQL ServerA simple and fast query to find the number of records/rows in every table in your database."
date: 2023-02-02T00:34:51+09:00
draft: false
weight: 40
---
A simple and fast query to find the number of records/rows in every table in your database.

```
select t.name TableName, i.rows Records from sysobjects t, sysindexes i
where t.xtype = 'U' and i.id = t.id and i.indid in (0,1) order by 2 desc;
```