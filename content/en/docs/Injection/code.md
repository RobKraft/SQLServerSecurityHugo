---
title: ".Net Code"
description: ".Net Code to Prevent SQL Injection"
date: 2020-01-28T00:34:51+09:00
draft: false
weight: 2
---

###### .Net Code to prevent SQL Injection

```
declare sqlstmt as string
sqlstmt = "Select * from people where email = '" + logonEntered + "'"
```
