---
title: "Worst Practices"
description: "A Checklist of the Worst Practices"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 11
---

{{< alert theme="danger" dir="ltr" >}}
**1. Allowing every user (or most users) to be SQL Server Administrators (members of the sysadmin role).**
**2. sa account is enabled and has no password.**
**3. sa account is enabled and has a simple password.**
**4. Allowing applications to use the sa account, or any account with sysadmin privileges in their connection strings.**
**5. Allowing every user (or most users) to be a database owner (dbo) in one or more databases.**
**6. Allowing a lot of users to be SQL Server Administrators (members of the sysadmin role).  A lot could mean more than one or more than 10 depending on your organization size.**
**7. Allowing a lot of users to be a database owner (dbo) in one or more databases.**
**8. Allowing anyone to use the sa account.**
**The rules above apply to SQL Server in shared environments such as production, test, or quality assurance.**
**9. Allowing any user, other than the regular user of the computer, to be a SQL Server Administrator (member of the sysadmin role) on a SQL Server instance used for development.  That SQL Server should not have TCP/IP enabled.**
**10. Running an [unsupported version of SQL Server](/configuration/version/), particularly SQL Server 2008 or earlier.**
**11. Running your SQL Server on an unsupported version of the operating system, particularly Windows Server 2008 or earlier, or Windows 8.1 or earlier.**
**12. Allowing applications exposed to the Internet with known SQL Injection vulnerabilities to continue to access SQL Server.**
**13. Having the 'sa' account enabled.**

----still working on this
**2. Ensure your version of SQL Server has the latest Cumulative Updates and Security Patches.**
**4. Ensure your operating system has the latest updates and Security Patches.**
**5. Ensure the firewall on your operating system has only the necessary ports open.**
**6. Avoid using well-known port 1433 for SQL Server, especially if the SQL Server is exposed to the Internet.**
**7. Do not install or disable services such as SSRS and SSIS that come with the SQL Server product if you don't use them.**
**8. Disable protocols available to SQL Server such as Named Pipes if they are not used.**
**10. Ensure the operating system accounts use strong authentication techniques.**
**11. Ensure the accounts used by the SQL Server services to log into the operating system allow the minimum operating system access required and use strong authentication techniques.**
**15. Disable XP_CMDSHELL, unless you need it and also are making sure that it is only used securely.**
**16. Ensure you are logging and regularly monitoring failed login attempts.**
**17. Ensure database backups are encrypted if they contain any sensitive data.**
{{< /alert >}}
