---
title: "Authentication"
description: "Validate the identity of the person or service attempting to connect."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 2
---

Configuring strong authentication for SQL Server might be the most important task a DBA performs.  Microsoft SQL Server is a very popular target for attacks by hackers, particularly by attempting to guess a password for the account named 'sa' and by using SQL Injection.

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

{{< alert theme="warning" dir="ltr" >}} In most cases, you should use Windows Authentication because Windows Active Directory offers better password management features than SQL Server Authentication.
{{< /alert >}}  

When using Windows Authentication, database administrators map groups from Windows Active Directory to Roles in SQL Server and use Active Directory to put people in groups that map to the roles needed.  

{{< alert theme="danger" dir="ltr" >}}
**1. Disable the 'sa' account and never use it!**
**2. Never allow any administrative level accounts to be used by an application.**
**3. Don't allow administrative level accounts to be used in non-production environments.**
{{< /alert >}}

* [Configure SQL Server to support Windows Authentication on Linux](https://www.mssqltips.com/sqlservertip/5075/configure-sql-server-on-linux-to-use-windows-authentication)


