---
title: "More"
description: "A Checklist For Hardening Your Server"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 10
---

https://www.elsevier.com/books/securing-sql-server/cherry/978-1-59749-947-7

[Monitoring SQL Server with Azure Sentinel](
https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/monitoring-sql-server-with-azure-sentinel/ba-p/)
[Setting Up SQL Audit for STIG Compliance](https://tracyboggiano.com/archive/2022/04/sql-audit-stig/)

https://docs.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-introduction

[Red-Gate SQL Server Security Blog](https://www.red-gate.com/simple-talk/databases/sql-server/security/)

Some SQL Server attacks of the past:
* [Cobalt Strike on 2022.2.22](https://www.bleepingcomputer.com/news/security/vulnerable-microsoft-sql-servers-targeted-with-cobalt-strike/)
* Example of hacking group that [targets source code](https://www.bleepingcomputer.com/news/security/microsoft-investigating-claims-of-hacked-source-code-repositories/)

Tools:
* [Windows Defender Application Control](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) to restrict when applications are allowed to run on a server.
* Microsoft's list of [security functions](https://docs.microsoft.com/en-us/sql/t-sql/functions/security-functions-transact-sql) useful in managing security.
* Microsoft's list of [security-related views](https://docs.microsoft.com/en-us/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)
* Microsoft's list of [security-related dynamic management views](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql)

Free Tools:
* [Red-Gate Free Tools](https://www.red-gate.com/products/free-tools)
* [Idera Free Tools](https://www.idera.com/productssolutions/freetools/)
* [Solar Winds Free Tools](https://www.solarwinds.com/free-tools)
* [Sentry One Plan Explorer](https://www.sentryone.com/plan-explorer)
* [ScaleSQL Free Tools](https://www.scalesql.com/sql-server-utilities/)
* [Microsoft Tools](https://learn.microsoft.com/en-us/sql/tools/overview-sql-tools?)


CIS:
1.1 [Latest Service Packs](/docs/configuration/version/)
1.2 [Dedicate server to SQL Server](/docs/configuration/operating/)
2.1 Ad Hoc
2.2 CLR enabled
2.3 Cross DB
2.4 Mail
2.5 Ole Auto
2.6 Remote Access
2.7 Remote Admin
2.8 Startup procs
2.9 Trustworth
2.10 - Protocols
2.11 - Ports
2/12 - Hide instance
2.13 - [disable sa] (/docs/auth/authentication/)
2/14 - [rename sa](/docs/auth/authentication/)
2.15 - autoclose off
2.16 - no sa login
2.17 - clr strict
3.1 Win Auth
3.2 Connect Perm
3.3 Orphan Users
3.4 SQL Auth contained dbs
3. - SQL Service acct
3.6 SQ Agent acct
3.7 Full text acct
3.8 default perms public
3.9 builtin groups not sql
3.10 win local groups not logins
3.11 public role msdb not granted
4.1 must change sql on
4.2 check exp on
4.3 check policy on
5.1 max err logs
5.2 default trace enabled
5.3 log failed
55.4 capture both audit
6.1 sanitize db input
6.2 clr assm perm
7.1 - sym key
7.2 asym key
8.1 browser service
