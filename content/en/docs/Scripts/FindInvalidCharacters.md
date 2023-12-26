---
title: "Find Invalid Characters"
description: "Search a column for invalid ASCII characters"
date: 2023-12-26T00:34:51+09:00
draft: false
weight: 60
---
This stored procedure looks for characters in an nvarchar field with what are usually, non-displayable characters, 
or non-ASCII characters, or basically, characters that English language speakers don't expect to see.


```
CREATE PROCEDURE sp_GetRowsWithInvalidCharacters
--  Rob Kraft 2023.12.26
    @TableName NVARCHAR(255),
    @ColumnName NVARCHAR(255)
AS
BEGIN
    DECLARE @DynamicSQL NVARCHAR(MAX);

    SET @DynamicSQL = 
        'SELECT TRIM(' + QUOTENAME(@ColumnName) + ') AS TrimmedValue,
         UNICODE(SUBSTRING(TRIM(' + QUOTENAME(@ColumnName) + '), PATINDEX(''%[^ !-~]%'' COLLATE Latin1_General_BIN, ' + QUOTENAME(@ColumnName) + '), 1)) AS UnicodeValue,
         ' + QUOTENAME(@TableName) + '.*
        FROM ' + QUOTENAME(@TableName) + '
        WHERE PATINDEX(''%[^ !-~]%'' COLLATE Latin1_General_BIN, ' + QUOTENAME(@ColumnName) + ') > 0
        ORDER BY UnicodeValue DESC;';

    EXEC sp_executesql @DynamicSQL;
END;

```

Example usage:
```
EXEC sp_GetRowsWithInvalidCharacters @TableName = 'mytablename', @ColumnName = 'mycolumnname';
```