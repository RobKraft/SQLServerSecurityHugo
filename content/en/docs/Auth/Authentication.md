---
title: "Authentication"
description: "Validate the identity of the person or service attempting to connect to SQL Server."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 2
---

###### Authenticating users and services and applications

Configuring strong authentication for SQL Server might be the most important task a DBA performs.  SQL Server is a very popular target for attacks by hackers, particularly by attempting to guess a password for the account named 'sa' and by using SQL Injection.

{{< alert theme="danger" dir="ltr" >}} **Disable the 'sa' account and never use it!**
{{< /alert >}}

Authentication is the process of validating that a user attempting to log in to SQL Server is really who they claim to be.  Often, the user is not a human, but is a service such as a web application.

In the early 21st century two methods of authentication were available, SQL Authentication and Windows Authentication.  Today, some deployments of SQL Server in cloud environments support a 'Managed Identity' option that is often the best because it can eliminate the need to manage credentials and secrets.  See [Azure SQL Authentication Options](https://docs.microsoft.com/en-us/sql/connect/ado-net/sql/azure-active-directory-authentication).

In your role as a DBA desiring to maximize security to prevent unwanted access into the databases, you should facilitate the adoption of good practices for authentication.  You need to identify what authentication you need to create for people as well as services for several use cases.  A common environment supports the following:

1. Accounts used by DBAs to administer SQL Server.
2. Accounts used by an application to connect to the database.
3. Accounts used by humans running adhoc reporting tools against the database.
4. Accounts in a development environment used by developers to create tables and other objects in databases.

Accounts can be authenticated either by SQL Server or by the operating system.  SQL Server authentication is not enabled by default.

{{< alert theme="warning" dir="ltr" >}} In most cases, you should use Windows Authentication because Windows Active Directory offers better password management features than SQL Server Authentication, and it is a little more secure.
{{< /alert >}}  

When using Windows Authentication, database administrators map groups from Windows Active Directory to Roles in SQL Server and use Active Directory to put people in groups that map to the roles needed.  

In addition to disabling the 'sa' account, you should also rename the 'sa' account.  Some people argue that disabling the 'sa' account is sufficient, and it may be in many cases.  But this site believes in the security principle of implementing [Defense in Depth](/docs/resources/principles/).  

{{< alert theme="danger" dir="ltr" >}}
**1. Disable the 'sa' account and never use it!**
**2. Never allow any administrative accounts to be used by an application.**
**3. Don't allow administrative accounts to be used in non-production environments by an application.**
{{< /alert >}}

###### SQL Statements
----
Run this SQL to determine if the 'sa' login has been renamed.
```
SELECT name FROM sys.server_principals WHERE sid = 0x01;
```
Run this SQL to rename the 'sa' login.  You can replace formerSaAccount with any name you desire.
```
ALTER LOGIN sa WITH NAME = formerSaAccount;
```
----
Run this SQL to determine if the 'sa' login has been disabled.  An 'is_disabled' value of 1 means the account is disabled.
```
SELECT name, is_disabled FROM sys.server_principals WHERE sid = 0x01;
```
Run this SQL to disable the 'sa' login.  Warning: If the 'sa' account has already been renamed, use the name from the query above in place of 'sa' below.  It is possible that a new account has been created and named 'sa'.  The important task is to rename the account that has a sid of 0x01.
```
ALTER LOGIN sa DISABLE;
```
----
###### Linux
* [Configure SQL Server to support Windows Authentication on Linux](https://www.mssqltips.com/sqlservertip/5075/configure-sql-server-on-linux-to-use-windows-authentication)


