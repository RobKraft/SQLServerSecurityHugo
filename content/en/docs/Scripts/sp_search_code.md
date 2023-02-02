---
title: "sp_search_code"
description: "Search all objects in SQL Server"
date: 2023-02-02T00:34:51+09:00
draft: false
weight: 50
---
Narayana Vyas Kondreddi wrote this proc long ago, but his site is gone.  I hope he doesn't mind if I continue providing his stored procedure here.  I recommend you put this in your master database so you can run it from any database.

```
CREATE PROCEDURE sp_search_code
--drop procedure dbo.sp_search_code
--Fixup by Rob Kraft 2023.2.2
(
@SearchStr varchar(100),
@RowsReturned int = NULL
)
AS
/*************************************************************************************************
Copyright © 1997 - 2002 Narayana Vyas Kondreddi. All rights reserved.
Purpose:To search the stored procedure, UDF, trigger code for a given keyword.
Written by:Narayana Vyas Kondreddi
http://vyaskn.tripod.com
Tested on: SQL Server 7.0, SQL Server 2000
Date created:January-22-2002 21:37 GMT
Date modified:February-17-2002 19:31 GMT
Email: vyaskn@hotmail.com
Examples:
To search your database code for the keyword 'unauthorized':
EXEC sp_search_code 'unauthorized'
To search your database code for the keyword 'FlowerOrders' and also find out the number of hits:
DECLARE @Hits int
EXEC sp_search_code 'FlowerOrders', @Hits OUT
SELECT 'Found ' + LTRIM(STR(@Hits)) + ' object(s) containing this keyword' AS Result
*************************************************************************************************/

BEGIN
SET NOCOUNT ON

SELECT DISTINCT USER_NAME(o.uid) + '.' + OBJECT_NAME(c.id) AS 'Object name',
CASE
WHEN OBJECTPROPERTY(c.id, 'IsReplProc') = 1
THEN 'Replication stored procedure'
WHEN OBJECTPROPERTY(c.id, 'IsExtendedProc') = 1
THEN 'Extended stored procedure'
WHEN OBJECTPROPERTY(c.id, 'IsProcedure') = 1
THEN 'Stored Procedure'
WHEN OBJECTPROPERTY(c.id, 'IsTrigger') = 1
THEN 'Trigger'
WHEN OBJECTPROPERTY(c.id, 'IsTableFunction') = 1
THEN 'Table-valued function'
WHEN OBJECTPROPERTY(c.id, 'IsScalarFunction') = 1
THEN 'Scalar-valued function'
WHEN OBJECTPROPERTY(c.id, 'IsInlineFunction') = 1
THEN 'Inline function'
END AS 'Object type',

'EXEC sp_helptext ''' + USER_NAME(o.uid) + '.' + OBJECT_NAME(c.id) + '''' AS 'Run this command to see the object text'

FROM syscomments c
INNER JOIN
sysobjects o
ON c.id = o.id
WHERE c.text LIKE '%' + @SearchStr + '%' AND
encrypted = 0 AND
(
OBJECTPROPERTY(c.id, 'IsReplProc') = 1 OR
OBJECTPROPERTY(c.id, 'IsExtendedProc') = 1 OR
OBJECTPROPERTY(c.id, 'IsProcedure') = 1 OR
OBJECTPROPERTY(c.id, 'IsTrigger') = 1 OR
OBJECTPROPERTY(c.id, 'IsTableFunction') = 1 OR
OBJECTPROPERTY(c.id, 'IsScalarFunction') = 1 OR
OBJECTPROPERTY(c.id, 'IsInlineFunction') = 1
OR xtype='v'
)

ORDER BY'Object type', 'Object name'
SET @RowsReturned = @@ROWCOUNT
END
```