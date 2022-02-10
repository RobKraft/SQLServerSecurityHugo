---
title: "Authentication"
description: "Validate the identity of the person or service attempting to connect."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 5
---

Configuring strong authentication for SQL Server might be the most important task a DBA performs.  Microsoft SQL Server is a very popular target for attacks by hackers, particularly by attempting to guess a password for the account named 'sa' and by using SQL Injection.

{{< alert theme="danger" dir="ltr" >}} **Disable the 'sa' account and never use it!**
{{< /alert >}}



