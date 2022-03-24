---
title: "Comprehensive Checklist"
description: "A Checklist For Hardening Your Server"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 4
---

{{< alert theme="danger" dir="ltr" >}}
**1. Ensure you are running a [supported version of SQL Server](/configuration/version/).**
**2. Ensure your version of SQL Server has the latest Cumulative Updates and Security Patches.**
**3. Ensure your SQL Server is running on a supported version of the operating system.**
**4. Ensure your operating system has the latest updates and Security Patches.**
**5. Ensure the firewall on your operating system has only the necessary ports open.**
**6. Avoid using well-known port 1433 for SQL Server, especially if the SQL Server is exposed to the Internet.**
**7. Do not install or disable services such as SSRS and SSIS that come with the SQL Server product if you don't use them.**
**8. Disable protocols available to SQL Server such as Named Pipes if they are not used.**
**9. Limit the number of accounts (people) that have Administator access to the operating system running SQL Server.**
**10. Ensure the operating system accounts use strong authentication techniques.**
**11. Ensure the accounts used by the SQL Server services to log into the operating system allow the minimum operating system access required and use strong authentication techniques.**
**12. Disable the 'sa' account and never use it!**
**13. Never allow any administrative accounts to be used by an application.**
**14. Don't allow administrative accounts to be used in non-production environments by an application.**
**15. Disable XP_CMDSHELL, unless you need it and also are making sure that it is only used securely.**
**16. Ensure you are logging and regularly monitoring failed login attempts.**
**17. Ensure database backups are encrypted if they contain any sensitive data.**
{{< /alert >}}

{{< alert theme="danger" dir="ltr" >}}
**There is more!  This site offers guidance for other steps you can take to strengthen the security of your SQL Server than just those contained on this list.**
{{< /alert >}}