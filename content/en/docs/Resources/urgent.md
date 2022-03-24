---
title: "The Urgent To Do List"
description: "A Checklist For Securing the Urgent Vulnerabilities."
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 2
---

If you have immediate concerns about the security of your SQL Servers, start with these actions.

{{< alert theme="danger" dir="ltr" >}}
**1. If your SQL Server is using the 'sa' account, [disable it](/docs/auth/authentication/).**
  * If you can't disable the 'sa' account, rename it.
  * If you are using the 'sa' account, even if renamed, make sure it has a strong password with ten or more characters.
  * If you can't assign a strong password to your 'sa' account, make sure your SQL Server is not exposed to the Internet.
  * Go no further until you have changed whatever is necessary to stop using the 'sa' account.

**2. Make sure no applications are [using Admin credentials](/docs/auth/authentication/) to connect to SQL Server.**
**3. If you are running a version of SQL Server older than SQL Server 2014, upgrade to the [most current version](/docs/configuration/version/) of SQL Server.**
**4. Make sure applications connecting to SQL Server are attempting to [stop SQL Injection](/docs/injection/sqli/), especially if exposed to the Internet.**  This could be a very large task.
**5. Make sure [connection strings](/docs/auth/connstrings/) are encrypted or using Windows Authentication.**
**6. Make sure sensitive data stored in your database [is encrypted](/docs/sensitive/whatsensitive/).**
**7. Make sure the [SQL Server services](/docs/auth/servicelogins/) are logging in to the OS with the least privileges needed.**
**8. If your SQL Server is exposed to the Internet, try to use a port other than [port 1433](/docs/configuration/ports/) to reduce the number of hacking attempts it receives.**
**9. Make sure your database [backups are encrypted](/docs/backups/backups/).**
**10. If xp_cmdshell is allowed, [disable it](/docs/configuration/sqlconfig/) if it is not used.  If it is used, make sure it is only used in secure contexts.**
{{< /alert >}}
