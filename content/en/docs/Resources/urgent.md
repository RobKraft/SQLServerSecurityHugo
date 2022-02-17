---
title: "The Urgent To Do List"
description: "A Checklist For Securing the Urgent Vulnerabilities."
date: 2020-01-28T00:34:51+09:00
draft: false
weight: -4
---

1. If your SQL Server is using the 'sa' account, disable it.
  * If you can't disable the 'sa' account, rename it.
  * If you are using the 'sa' account, even if renamed, make sure it has a strong password with ten or more characters.
  * If you can't assign a strong password to your 'sa' account, make sure your SQL Server is not exposed to the Internet.
  * Go no further until you have changed whatever is necessary to stop using the 'sa' account.
2. If your SQL Server is exposed to the Internet, try to use a port other than port 1433 to reduce the number of hacking attempts it receives.
3. If you are running a version of SQL Server older than SQL Server 2014, upgrade to the most current version of SQL Server.
4. If xp_cmdshell is allowed, disable it if it is not used.  If it is used, make sure it is only used in secure contexts.
5. Make sure no applications are using Admin credentials to connect to SQL Server.
6. Make sure connection strings are encrypted or using Windows Authentication.
7. Make sure the SQL Server services are logging in to the OS with the minimal permissions needed.
8. Make sure applications connecting to SQL Server are attempting to stop SQL Injection, especially if exposed to the Internet.
9. Make sure sensitive data stored in your database is encrypted.
10. Make sure your database backups are encrypted.
