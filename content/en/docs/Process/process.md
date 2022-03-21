---
title: "Ongoing Processes"
description: "Security is not something to implement and forget. It must be monitored."
date: 2020-01-28T00:34:51+09:00
draft: false
weight: 2
---

Security is not something to implement and forget. You need to spot-check configurations and review logs periodically or possibly even continuously depending on your risk profile.

People may open a port or change a configuration temporarily but forget to change it back.  Hackers may discover an opening you were unaware of but their activity is getting recorded in your logs.  The installation of a new server or enablement of a new feature may not comply with your desired rules.  Therefore we need to keep reviewing our environment to make sure our security posture remains hardened.

Many tools and features to aid your monitoring efforts are mentioned elsewhere on this site, but are repeated here for your convenience.

###### Logging and Monitoring Tools

* SQL Server Error Log
* Windows Application Event Log
* Extended Events
* Stored procedures (Sp_who)
* SQL Server [Vulnerability Assessment](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-vulnerability-assessment)
* SQL Server [Data Discover and Classification](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-data-discovery-and-classification)

Because there are many things that need to be monitored, you may want to consider third-party tools that aggregate monitoring from many sources into a single dashboard that includes immediate notification when values change or thresholds are exceeded.

1. Physical environment security
2. OS patched
3. Cloud if cloud hosted or ISP hosted -physical and network and shared environs

https://www.sqlshack.com/top-10-security-considerations-sql-server-instances/

https://www.red-gate.com/simple-talk/databases/sql-server/security/what-to-monitor-for-sql-server-security/

https://www.mssqltips.com/sqlservertip/3159/sql-server-security-checklist/

https://www.technig.com/20-best-sql-server-monitoring-tools/
https://docs.microsoft.com/en-us/sql/relational-databases/security/securing-sql-server

* [Idera Security Suite](https://www.idera.com/productssolutions/sqlserver/sql-server-security-suite)
apexsql


**Examples to come of things you should monitor, the tools SQL server provides and also tools from other vendors than can be very helpful.**