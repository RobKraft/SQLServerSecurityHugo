---
title: "Ongoing Processes"
description: "Security is not something to implement and forget. It must be monitored."
date: 2022-02-27T00:34:51+09:00
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
  * https://docs.microsoft.com/en-us/sql/relational-databases/security/auditing/sql-server-audit-database-engine?view=sql-server-ver15
* SQL Server Agent Error Logs 
* SQL Server Agent Job History
* Stored procedures (Sp_who)
* Track SQL Logins: https://www.sqlshack.com/using-extended-events-review-sql-server-failed-logins/
* C2 Audit Logs
* SQL Server [Policy Based Management](https://docs.microsoft.com/en-us/sql/relational-databases/policy-based-management/administer-servers-by-using-policy-based-management?view=sql-server-ver15)
* SIEM (Security Information and Event Management) Tools

Because there are many things that need to be monitored, you may want to consider third-party tools that aggregate monitoring from many sources into a single dashboard that includes immediate notification when values change or thresholds are exceeded.

1. Physical environment security
2. OS patched
3. Cloud if cloud hosted or ISP hosted -physical and network and shared environs

###### Assessments

What you may be engaged in right now, reading the content of this website, is an assessment of the security of your SQL Server and its data.  Here are some ways to do assessments:

* Figure out what you think you need to know and fix anything you find that is insecure,
* Follow a checklist or use a tool (software package) to perform a one-time assessment,
* Schedule software to run automatically that assesses the security of your of your environment,
* Hire a company to audit your environment and perform an assessment

This web site has some checklists, but for a small amount of money there are many software vendors that provide products that can continually monitor your environment and notify you when things change.  You can even do some of this with Policy Management built into SQL Server.

###### Center for Internet Security Benchmarks

The Center for Internet Security (CIS) maintains benchmarks for many software products including [SQL Server](https://www.cisecurity.org/benchmark/microsoft_sql_server).  The benchmarks include a free checklist of hardening recommendations.  In addition, CIS provides a tool, CIS-Cat Pro, you can use to automated assessment of your adherence to benchmarks.  The configurable tool allows you to exclude rules that don't apply.  They also offer CIS-CAT Lite for free, but it doesn't include any checks for SQL Server.

https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-server-security-best-practices?view=sql-server-ver15
https://www.mssqltips.com/sqlservertip/2887/sql-server-security-audit-part-2-scripts-to-help-you-or-where-can-you-find-more-information/

https://isqlplus.com/sql-server/sql-server-security-scripts/


* [All In One SQL Audit Script](https://thedataguy.in/sql-server-security-audit-script/)
* [Powershell Script SQL Server Audit](https://blog.pythian.com/sql-server-security-review-using-powershell/)

https://www.sqlshack.com/top-10-security-considerations-sql-server-instances/

https://www.red-gate.com/simple-talk/databases/sql-server/security/what-to-monitor-for-sql-server-security/

https://www.mssqltips.com/sqlservertip/3159/sql-server-security-checklist/

https://www.technig.com/20-best-sql-server-monitoring-tools/
https://docs.microsoft.com/en-us/sql/relational-databases/security/securing-sql-server

* [Idera Security Suite](https://www.idera.com/productssolutions/sqlserver/sql-server-security-suite)
apexsql


**Examples to come of things you should monitor, the tools SQL server provides and also tools from other vendors than can be very helpful.**

* SQL Server [Vulnerability Assessment](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-vulnerability-assessment)
* SQL Server [Data Discover and Classification](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-data-discovery-and-classification)

* [What to monitor](https://www.red-gate.com/simple-talk/databases/sql-server/security/what-to-monitor-for-sql-server-security/)

SQL Server provides logs other than those mentioned above that you probably want to monitor and review occasionally.  The other logs are unlikely to contain items of interest to security professionals, but may be helpful for troubleshooting other problems.  DatabaseMail, SSRS, SSIS, etc.
