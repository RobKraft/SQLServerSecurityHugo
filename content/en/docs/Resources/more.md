---
title: "More"
description: "A Checklist For Hardening Your Server"
date: 2020-01-28T00:34:51+09:00
draft: false
weight: -4
---

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

Vulnerablities:
https://stack.watch/product/joomla/joomla/

https://www.cvedetails.com/product/251/Microsoft-Sql-Server.html?vendor_id=26