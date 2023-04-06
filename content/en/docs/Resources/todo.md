---
title: "Web Site To Do List"
description: "Content planned for development for the site"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 20
---

* https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-server-security-best-practices?view=sql-server-ver15
* https://www.mssqltips.com/sqlservertip/2887/sql-server-security-audit-part-2-scripts-to-help-you-or-where-can-you-find-more-information/
* Scripts for finding Orphan Users and deleting them
* Scripts for listing all accounts with server roles
* Good stuff here: https://www.sqlshack.com/sql-server-audit-overview/
* Application Roles
* Proxy account for XP_CMDSHELL: https://www.mssqltips.com/sqlservertip/2143/creating-a-sql-server-proxy-account-to-run-xpcmdshell/
* Tip about having applications, especially .Net, pass their app name to SQL Server
* Checklist for ultimate security
* Article about levels of security: 1) Internal, not sensitive, 2) Internal, sensitive, 3) External not sensitive, 4) External and sensitive (yikes)
* Articles discussing options for resolving specific security risks
  * Example 1
  * Example 2
* Articles discussing design options for specific environments
  * We have both desktop and web apps on the Internet as well as reporting tools
  * Our web site lets users ORDER BY dynamically.  How can we safely construct such SQL against SQL Injection?
  * others
* Articles describing how to make some specific changes
* An article with tools/checklists to quickly use to assess an environment for free
* A downloadable spreadsheet checklist template
* An api to call to get a list of queries in json to run
* Links to videos by others about specific items
* Page listing each security feature in SQL Server and where/how to use it
* Page listing each SQL Server feature and how it is vulnerable
* How to guide for each item on the urgent list
* Overview of AWS SQL Server options
* Overview of Azure SQL Server options
* Best security practices for AWS and Azure
* Links to libraries to help protect against SQL Injection
* Info about services I can offer
* Picture of the SQL Server environment and surface area
* More articles in Protecting Sensitive data
* More links for good guidance in Compliance Guidelines
* More info about SQL Browser
* More info about other SQL Server Services (SSRS, SSIS, and other tools)
* Azure Data Studio vs SSMS
* SQL Inspector
* More about How hackers attack
* A lot more about Policy Based Management
* Images and step by step instructions for everything?
* FAQ: What is second order SQL Injection (2nd order sql injection)?
* Certificate management and security
* Article about "Execute As" function
* Securing XP_Cmdshell - https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql?view=sql-server-ver15
* Guidance: MS SQL Install: https://docs.microsoft.com/en-us/sql/sql-server/install/security-considerations-for-a-sql-server-installation?view=sql-server-ver15
* Guidance: Use NTFS for file system
* Guidance: Disable netbios and SMB ports
* Guidance: Dont install on Domain Controller
* Article about Pen Tests of ports/servers
* Article about Pen Tests for SQL Injection, and static testing and products
* Article about Hard drive scans of config files
* Article about Github repo scans of source code for conn strings
* Article about Google dorks
* A page describing a devops pipeline to secure everything.
* Dev training about risks and proper coding
* Pair programming
* Static code analyzers
* Code reviews
* Code frameworks, parameters, utilities, constructing SQL, etc.
* Automatice analyzers on checkins
* Custom analyers
* SQL in code vs stored procs
* Dev environment permission control
* DevOps protection of conn strings for deploy
* Cloud security
* Log Monitoring
* Firewalls, IDS, IPS
* Environ config monitoring - perms monitoring
* Auditing
* More about SQL Server Agent security
* Security for SQL Server Service Broker - future?
* Security of SQL Server Profiler future?
* Wireshark
* SQL Server Reporting Services - future?
* SSIS, SSAS, etc.



\should set "Encrypt=true" property in client connection string, and even better the DBA should install a proper SSL certificate in SQL Server and set option to enforce all client connections to use encryption. It's essentially the same concept as HTTPS connections on the web.

Tools List:

* [DBATools.IO](https://dbatools.io/) - A free curated library of 500+ useful Powershell scripts.
* [SQLServer-DBA Powershell scripts](https://www.sqlserver-dba.com/2012/07/powershell-scripts-for-dba.html) - Dozens of helpful Powershell scripts
* https://glennsqlperformance.com/resources/ 
* https://www.cisecurity.org/benchmark/microsoft_sql_server
* https://www.brentozar.com/blitz/
* https://ola.hallengren.com/
* https://www.red-gate.com/products/free-tools
* https://www.idera.com/productssolutions/freetools
* https://doccolabs.com/
* https://sqlstudies.com/free-scripts/
* https://www.cisa.gov/free-cybersecurity-services-and-tools
* [System File Checker](https://docs.microsoft.com/en-us/troubleshoot/windows-server/deployment/system-file-checker) may be able to identify files that have been replaced with malware versions.
* https://www.solarwinds.com/sql-sentry
* Idera
* Redgate - sql monster
* sql power tools
* sql sentry
* quest - spotlight
* Quest has a product called [ApexSQL](https://apexsql.com/) that assists your adherence to many compliance standards.
* sql backup master  - https://www.sqlbackupmaster.com/features

* Set up alerts to notify you of excessive failed login attempts from [SQLUnderCover.com](https://sqlundercover.com/2023/03/29/using-sql-alerts-to-spot-suspicious-activity-in-sql/) 

Free stuff to do right away:

* SQL Server [Vulnerability Assessment](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-vulnerability-assessment)
* Sp_Blitz
* [Microsoft Assessment](https://www.mssqltips.com/sqlservertip/7435/check-sql-server-best-practice-settings-invoke-sqlassessment/)

Checklist for new SQL Server Installation.  Security and Perf and all:
* Automate backups
* Include DBCC CheckDB
* Include index rebuilds
* 
https://www.sqlshack.com/best-practices-for-configuring-newly-installed-sql-server-instances/
https://blog.pythian.com/sql-server-default-configurations-change/
https://www.brentozar.com/archive/2013/09/five-sql-server-settings-to-change/

