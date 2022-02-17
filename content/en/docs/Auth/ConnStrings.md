---
title: "Connection Strings"
description: "Guidance for securely managing connection strings."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 10
---

When a human connects to a database, your software can prompt them for their credentials, but when an application connects to a database, that is usually not an option.  Applications, like people, have two options for authentication.  One is to authenticate by providing a login and password; the other is to autenticate using the same credentials the application has already logged into the operating system with, which is known as integrated security.

Using Integrated Security (aka Windows Authentication) does not require credentials to be stored in a file, or the registry, or in a database.  Therefore it has an advantage over using a Login and Password because developers and people deploying the software don't need to take steps to protect and encrypt Login credentials.

There are drawbacks to Integrated Security.  One drawback is when you have desktop applications using Integrated Security, which results in the applications connecting to SQL Server with the permissions of the user logged into the OS.  Application developers often put logic into their programs to prevent data modifications and deletes based on the state of the data, but a user with Integrated Security could use another tool to connect to the SQL Server database and edit the data directly in the tables.  

{{< alert theme="danger" dir="ltr" >}} **Disable the 'sa' account and never use it!**
{{< /alert >}}