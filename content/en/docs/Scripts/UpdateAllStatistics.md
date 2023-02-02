---
title: "Update the index statistics for every index on every table."
description: "Update the index statistics for every index on every table."
date: 2023-02-02T00:34:51+09:00
draft: false
weight: 14
---
Update the index statistics for every index on every table

```
sp_MSforeachdb 'use [?]; exec sp_updatestats'
```