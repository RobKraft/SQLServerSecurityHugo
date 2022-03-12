---
title: "Connection Strings"
description: "Guidance for managing connection strings."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 10
---

###### Securing connection strings in applications

When a human connects to a database, the software can prompt them for their credentials, but when an application connects to a database, that is usually not an option.  Applications, like people, have two options for authentication.  One is to authenticate by providing a login and password; the other is to autenticate using the same credentials the application has already logged into the operating system with, which is known as integrated security.

{{< alert theme="info" dir="ltr" >}} **Every application requires a connection string to connect to a database.**
{{< /alert >}}

Every application must provide credentials in order to connect to a database.  That set of credentials, along with the server address, port it is running on, and software driver, are collectively referred to as the 'connection string'.  The 'connection string' is all the information an application needs to connect to a SQL Server.  Connection strings are rarely hard-coded into programs because that makes it more difficult to change them.  They are often stored external to the program.  Whether hard-coded or stored externally, if the connection string contains a password or other secret that allows it to connect to SQL Server, that connection string needs to be secured.

Using Integrated Security (aka Windows Authentication) does not require credentials to be stored in a file, or the registry, or in a database.  Therefore it has an advantage over using a Login and Password because developers and people deploying the software don't need to take steps to protect and encrypt Login credentials.

There are drawbacks to Integrated Security.  One drawback, when you have desktop applications using Integrated Security, is that users can bypass the applications you wrote to allow them to read and modify data in the database.  Products like SQL Server Management Studio, Microsoft Access, Microsoft Excel, Crystal Reports, and hundreds of other products can connect to the SQL Server database and take any action allowed by their Integrated Security permissions.  This allows people to bypass rules that make sure data is modified correctly that your coded into the programs you expected people to use.  Application developers often put logic into their programs to prevent data modifications and deletes based on the state of the data.

Web applications may use Integrated Security with less risk when the web application and SQL Server are in the same domain and the web application threads do not run using the credentials of each user logged into the web application.  This web application design approach is rare, but used to be more common and is still possible, especially with the IIS web server.  Most web applications today run in a security context defined by the web application and shared by all users, which in turn requires logic in the application to determine what data each user is allowed to view and manipulate.

Examples of connection strings may be found at [ConnectionStrings.com](https://www.connectionstrings.com/sql-server/).

{{< alert theme="info" dir="ltr" >}}**When a connection string uses Integrated Security, you don't need to take steps to secure the connection string.**
{{< /alert >}}

{{< alert theme="warning" dir="ltr" >}}**When a connection string contains credentials, you need to take steps to secure those credentials.
{{< /alert >}}

One of the most common places to store connection string information is in a file named web.config for web applications, or an application config file for desktop applications.  Encrypting the connection string section of a .Net config file is fairly simple and a lot of tutorials and videos exist online to guide you through the steps.  Be aware that the encryption uses machine keys that are part of the operating system.  This means a config file encrypted on one server can't be copied and used in another server, as is often desired in web farms, unless every server in the web farm has the same machine keys.  Also, server instances that are frequently destroyed and rebuilt, such as in cloud environments, need to re-encrypt the config files or re-install the same machine keys back into the new instance of the server built from the base image.

Developers sometimes store connection string information in text files, .ini files, or in the computer registry.  Most of these practices are very bad, unless those credentials can be encrypted in their external locations.  Connection strings stored in compiled executables are also bad as the can be easily discovered in most cases by opening the executable with a simple program like notepad.

Better security for connection strings is one of the benefits provided by most cloud development environments.  Clouds such as AWS and Azure provide options similar to Integrated Security that allow your application to connect to a cloud hosted database by assigning a security role to the cloud service that needs to access the database.  Prior to the Active Directory Managed Identity option available in clouds, many deployments stored connection strings in Environment variables in the cloud.  These environment variables are usually secure and stored encrypted, but are not as easy to manage as using Active Directory Managed Identity.

{{< alert theme="danger" dir="ltr" >}} **Make sure your connection strings are always encrypted if they contain credentials.**
{{< /alert >}}

A lot of malware scans computer hard drives for config files and application source code looking for database connection strings.

Some developers hard code connection strings, or include the connection strings in code that is commented but still within the source code.  This is dangerous especially when your source code is stored in a cloud repository such as github or bitbucket.  It is very easy to search all public github repositories for connection strings.  Even when your repository is private there is a risk it will get exposed publicly by mistake, or forked or copied into a public libary.

{{< alert theme="danger" dir="ltr" >}} **Do not use the same credentials for production servers that you use for non-production servers.**
{{< /alert >}}

Consider using [Secret Manager](https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets) for new .Net core development.


Do you have a complicated scenario that leaves you feeling their is no good secure solution?  Contact me, I've done this a lot of ways for three decades and am happy to consult at reasonable rates.


{{< alert theme="danger" dir="ltr" >}}
**1. Make sure your connection strings are always encrypted if they contain credentials.**
**2. Never commit connection string credentials into source code repositories.**
**3. Avoid giving the SQL Server Login connecting through the connection string any permissions other than the ability to read and write data in tables and execute stored procedures.**
**4. If the application requires the ability to create or modify database tables, only grant the minimal permissions the application needs.**
**5. Do not give an application database owner permissions or any SQL Server system level permissions.**
{{< /alert >}}

{{< alert theme="warning" dir="ltr" >}}
**6. In cloud deploys, use the cloud provided integrated security through service roles and the cloud's Identity and Access Management (IAM).**
**7. On premise, strive to use Integrated Security for applications connecting to SQL Server.**
**8. When connection strings require a User ID and Password, make sure to use a strong password at least 12 characters long.**
**9. When connection strings require a User ID and Password, create a User ID that is also long and cryptic.**
{{< /alert >}}
