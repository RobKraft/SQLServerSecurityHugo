---
title: "Refresh the metadata for every view in the database."
description: "Refresh the metadata for every view in the database."
date: 2023-02-02T00:34:51+09:00
draft: false
weight: 12
---
Refresh the metadata for every view in the database.

```
SET NOCOUNT ON
DECLARE @SQL varchar(max) = ''
SELECT @SQL = @SQL + 'print ''Refreshing --> ' + u.name + '.' + o.name + ''' 
EXEC sp_refreshview [' + u.name + '.' + o.name + '];'
FROM sysobjects o inner join sysusers u  on o.uid=u.uid WHERE type = 'V' order by u.name
EXEC(@SQL)
go
```