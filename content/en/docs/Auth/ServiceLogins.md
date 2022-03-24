---
title: "SQL Server Service Accounts"
description: "Guidance for accounts used by SQL Server to log in to the Operating System."
date: 2022-02-27T00:36:14+09:00
draft: false
weight: 11
---

###### Securing the accounts used by SQL Server to log in to the OS

Like most windows services, the SQL Server service needs an operating system account to use to log in to the operating system.  This account should only be given the permissions necessary for the features of SQL Server you use to work correctly.  By limiting the permissions of this account, you also limit the things a hacker may have accomplished if they have managed to hack into your SQL Server.  In the early days of SQL Injection attacks on SQL Servers, hackers used the XP_CMDSHELL function of SQL Server to execute operating system commands and the SQL Servers were often running using accounts with windows admistrator or Domain administrator privileges.  This allowed those hackers to take over all the computers in a company.




Todo service accounts:
https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?view=sql-server-ver15
 


Additional Hardening steps you can take:
* Dedicate the server to running SQL Server.  Dedicating servers to a single product (SQL Server
, Exchange, Web server, etc.) reduces the number of ports, directories, services, and credentials that need to be exposed and monitored for a server.  It reduces the risk that an infiltration from one product opens a way to infiltrate other products on the same server.
* Use a credential manager, including features in Active Directory, to automatically change credentials periodically for the service account.
Credential management automated when deployed to prod.
{{< alert theme="danger" dir="ltr" >}} **Disable the 'sa' account and never use it!**
{{< /alert >}}

https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?view=sql-server-ver15