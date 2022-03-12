---
title: "App Login Accounts"
description: "Guidance for accounts used by applications."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 8
---

###### Accounts used applications connecting to SQL Server

Limit the permissions granted to logins used by applications to only do actions that the application is expected to do.  Decades ago, applications used the sa account to connect to the database.  This made it easy to configure, but opens the door for a SQL Injection vulnerability to take over the SQL Server, the underlying operating system, and the entire network.

Few applications need more permissions that the ability the four traditional CRUD (Create, Read, Update, and Delete) permissions, along with the ability to execute stored procedures.  A better acronym than CRUD, for SQL applications, would be SIUD (Select, Insert, Update, and Delete).

SQL Server provides built-in roles that work well for a lot of applications.  db_datareader grants Select permission to all tables in a database, and db_datawriter grants Insert, Update, and Delete permissions to all tables in a database.  You can, and should, also create your own Database Roles if those provided don't work for your application.

You should probably never grant applications any of the built-in Server Roles such as dbcreator, securityadmin, and sysadmin, unless you have purchased a third-party package to audit your databases or manage your backups and it requires Server Roles.  

You also should probably never grant applications the db_owner role in a database.

These guidelines apply to non-production environments as well as production environments.  In non-production environment, developers (humans) may need to have elevated permissions to create tables and stored procedures, but the applications running in non-production environments should not run with such elevated privileges to reduce the risk that developers design their application in a way to need more permissions.

It is generally better to predefine permanent "temporary" tables than to allow the application to create and delete tables on the fly; but that does not work in all scenarios.

Consider designing applications in ways that minimize the permissions needed in the database.

{{< alert theme="danger" dir="ltr" >}} **Disable the 'sa' account and never use it!**
{{< /alert >}}