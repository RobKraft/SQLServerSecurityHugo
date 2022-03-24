---
title: "More"
description: "A Checklist For Hardening Your Server"
date: 2020-01-28T00:34:51+09:00
draft: false
weight: 10
---


SQL Server Agent security
SQL Server Service Broker - future?
SQL Server Profiler future?
SQL Server Reporting Services - future?
SSIS, SSAS, etc.

An installation checklist for hardened install

A page describing a devops pipeline to secure everything.
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
* CIS and other tools

https://www.brentozar.com/blitz/
https://ola.hallengren.com/
https://www.red-gate.com/products/free-tools
https://www.idera.com/productssolutions/freetools
https://doccolabs.com/
https://dbatools.io/
https://sqlstudies.com/free-scripts/
https://www.cisa.gov/free-cybersecurity-services-and-tools
 
* Quest has a product called [ApexSQL](https://apexsql.com/) that assists your adherence to many compliance standards.

Physical security
SQL Browser service
Pen Tests of ports/servers
Hard drive scans of config files
Github repo scans of source code for conn strings
Google dorks

https://www.elsevier.com/books/securing-sql-server/cherry/978-1-59749-947-7


History of attacks:
2022.2.22: https://www.bleepingcomputer.com/news/security/vulnerable-microsoft-sql-servers-targeted-with-cobalt-strike/

https://docs.microsoft.com/en-us/sql/sql-server/install/security-considerations-for-a-sql-server-installation?view=sql-server-ver15
Use NTFS for file system
Disable netbios and SMB ports
Dont install on Domain Controller

Policies

\should set "Encrypt=true" property in client connection string, and even better the DBA should install a proper SSL certificate in SQL Server and set option to enforce all client connections to use encryption. It's essentially the same concept as HTTPS connections on the web.

Images and step by step instructions for everything?

FAQ: What is second order SQL Injection (2nd order sql injection)?

Harden your servers: https://www.upguard.com/blog/the-windows-server-hardening-checklist

Email mailing lists:
* newsletter@mssqltips.com
* Brent Ozar
* SQLServerCentral.com

https://docs.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-introduction

SQL Server Security by Robert Sheldon:
https://www.red-gate.com/simple-talk/devops/data-privacy-and-protection/introduction-to-sql-server-security-part-1/


[Red-Gate SQL Server Security Blog](https://www.red-gate.com/simple-talk/databases/sql-server/security/)

Vulnerablities:
https://stack.watch/product/joomla/joomla/

https://www.cvedetails.com/product/251/Microsoft-Sql-Server.html?vendor_id=26

Microsoft's [SQL Server Security Best Practices](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-server-security-best-practices)

Free stuff to do right away:
* SQL Server [Vulnerability Assessment](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-vulnerability-assessment)

Example of hacking group that [targets source code](https://www.bleepingcomputer.com/news/security/microsoft-investigating-claims-of-hacked-source-code-repositories/)

Certificate management and security

Tools:
* [Windows Defender Application Control](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) to restrict when applications are allowed to run on a server.
* Microsoft's list of [security functions](https://docs.microsoft.com/en-us/sql/t-sql/functions/security-functions-transact-sql) useful in managing security.
* Microsoft's list of [security-related views](https://docs.microsoft.com/en-us/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)
* Microsoft's list of [security-related dynamic management views](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql)

secure xp_cmdshell: https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql?view=sql-server-ver15

simpler checklist: https://www.mssqltips.com/sqlservertip/3159/sql-server-security-checklist/

https://glennsqlperformance.com/resources/

https://www.cisecurity.org/benchmark/microsoft_sql_server

https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql?view=sql-server-ver15

Execute As function

powershell script sites



CIS:
1.1 [Latest Service Packs](/docs/configuration/version/)
1.2 [Dedicate server to SQL Server](/docs/configuration/operating/)
2.1 Ad Hoc
2.2 CLR
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


Principle of Least Privilege

Cert https://www.cisa.gov/uscert/ics/Abstract-Defense-Depth-RP


