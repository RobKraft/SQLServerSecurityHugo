---
title: "Installation Checklist"
description: "A Checklist For Installing Your SQL Server"
date: 2020-01-28T00:34:51+09:00
draft: false
weight: 5
---

{{< alert theme="danger" dir="ltr" >}}
**1. Harden your [physical environment](/docs/configuration/physical/).**
**2. Harden your computer BIOS or UEFI Firmware if needed.**
**3. Harden your [Operating System](/docs/configuration/operating/).**
**3.1 Identify or create a group in Active Directory that will be in the SQL Server Administrator role.  Assign minimal people to that role.**
**3.2. Ensure the firewall on your operating system has only the necessary ports open.**
**4. Install the most current version of SQL Server.  Only install the components you need.**
**4.1 Long ago, there was some security benefit to installing SQL Server and the databases on drives other than the C:\ drive.  The value of doing so is trivial today.  However, you may consider doing so for performance and management reasons.**
**4.2 Use a separate account for each service installed.  Use [Managed Service Accounts](/todo).  Disable SQL Server Browser.**
**4.3 Use Windows authentication mode (not Mixed Mode).  Select the Active Directory group you created for SQL Server Administrators.**
**5. Ensure your version of SQL Server has the latest Cumulative Updates and Security Patches.**
**6. Use SQL Configuration Manager to change the port number SQL Server listens on.(in mmc) todo**
**7. Use SQL Configuration Manager to disable protocols available to SQL Server such as Named Pipes if they are not used.**
**8. Disable the 'sa' account and never use it!**
**9. Disable XP_CMDSHELL, and other configured features.**
**10. Ensure you are logging and regularly monitoring failed login attempts.**
**11. Create roles for applications and developers.**
**12. Ensure database backups are encrypted if they contain any sensitive data.**
{{< /alert >}}
