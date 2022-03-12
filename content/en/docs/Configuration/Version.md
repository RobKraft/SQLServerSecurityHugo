---
title: "Version of SQL Server"
description: "Guidance for specific versions of SQL Server."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 5
---

###### Use a supported version of SQL Server

Microsoft releases a new version of SQL Server roughly every two years.  Although you may not need any of the features provided in the new version, it is important to upgrade to a version of SQL Server that is still under support in order to obtain security fixes, especially if your SQL Server is exposed to the Internet.

If a security vulnerability is discovered in a version of SQL Server that is no longer under support, Microsoft will probably not provide a patch to fix the vulnerability, and you can be sure hackers will attempt to exploit it.

Microsoft offers you the ability to buy [Extended Security Support](https://docs.microsoft.com/en-us/sql/sql-server/end-of-support/sql-server-extended-security-updates), but you must purchase these before the security vulnerability is found and even extended support will eventually no longer be offered.

Additional Resources:

* [Learn about SQL Server product "End of life"](https://www.lansweeper.com/eol/a-comprehensive-guide-to-sql-server-end-of-life/)

{{< alert theme="info" dir="ltr" >}} **Support for SQL Server 2012 ends July 12, 2022
Support for SQL Server 2014 ends July  9, 2024**
{{< /alert >}}