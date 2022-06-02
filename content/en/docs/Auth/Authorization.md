---
title: "Authorization"
description: "Configure the permissions the connected user or service is allowed to perform."
date: 2022-02-27T00:36:14+09:00
draft: false
enableToc: false
weight: 4
---

###### Authorizing users and services logged into SQL Server 

{{< alert theme="danger" dir="ltr" >}}
**Grant the least privileges needed to each account.**
{{< /alert >}}

Most applications need no permissions other than the ability to perform CRUD operations (Insert, Select, Update, and Delete).  These permissions can be provided using the built-in db_datareader and db_datawriter roles.

Work with developers to make sure their applications do not need the ability to create tables or other structures in the database.  Use one role for applications that need to read and write data.  

For adhoc reporting tools, create a group and assign the db_datareader permission to the group and use Active Directory to control group membership.

Do not use db_datareader when your database has sensitive information that should only be accessible through the application and not reporting tools.

###### Specific Guidance

* Always follow the principle of [least privilege](/docs/resources/principles/).
  * If a person or service only needs to back up a database, add them to the DBCreator role (not the sysadmin role)
* Most users of applications, both services and humans, need nothing more than the public role in SQL Server, and the db_datareader and db_datawriter roles in a database.  
  * Add only Active Directory groups to the db_datareader and db_datawriter roles.
  * Create another Database Role for StoredProcedures and give the Execute permission on all of your application stored procedures to that role.
    * Add the Active Directory groups to the new StoredProcedures database role as needed.
* Assign Active Directory roles to roles in SQL Server.  Don't assign individual Active Directory user accounts to roles in SQL Server.


