---
title: "Authorization"
description: "Configure the permissions the connected user or service is allowed to perform."
date: 2020-01-28T00:36:14+09:00
draft: false
enableToc: false
weight: 4
---

###### Authorizing users and services logged into SQL Server 

{{< alert theme="danger" dir="ltr" >}}
**1. Disable the 'sa' account and never use it!**
**2. Grant the least privileges needed to each account.**
{{< /alert >}}

Most applications need no permissions other than the ability to perform CRUD operations (Insert, Select, Update, and Delete).  These permissions can be provided using the built-in db_datareader and db_datawriter roles.
Work with developers to make sure their applications do not need the ability to create tables or other structures in the database.
Use one role for applications that need to read and write data.  
For adhoc reporting tools, create a group and assign the db_datareader permission to the group and use Active Directory to control group membership.
Execute Stored Procs.
Do not use db_datareader when your database has sensitive information that should only be accessible through the application and not reporting tools.
