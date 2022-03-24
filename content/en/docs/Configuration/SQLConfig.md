---
title: "Configuration"
description: "Guidance for enabling and disabling of SQL Server Features"
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 8
---

###### Only install services and features you intend to use

The SQL Server installer includes multiple products and features.  You may desire to install all the products and features to explore them, but you should always uninstall any products and features you don't intend to use.  On production servers, you should only install the products and services that you use; not products and features that you "might" use.  This guidance applies to all products and their features, not just SQL Server.  By choosing to only install what you will use, you are reducing the "attack surface" available to hackers that might allow them to find vulnerabilities on your server.  If you are not using a product, you should not install the product, because if you do install the product, malware may find the product and also discover a vulnerability in it that allows them to compromise and take over your server.  

Some of the products that you can install with SQL Server include:

* SQL Server Reporting Services (SSRS)
* SQL Server Integration Services (SSIS)
* SQL Server Analysis Services (SSAS)

Don't install them if you don't use them.  Even if you do install them, you may desire to install them on different servers than the server running SQL Server.

SQL Server includes a lot of features that can be enabled or disabled.  You should disable features you are not using, partially because it can improve performance, but also because some features can increase security risks.

The feature a SQL Server administrator should be most concerned about is a function called XP_CMDSHELL.  If malware infects your SQL Server the first thing it looks for is the ability to exploit XP_CMDSHELL.  If it can use XP_CMDSHELL, it can run commands against the underlying operating system and possibly install malware and take over the entire server.  All the automated hacking tools are coded to attempt to exploit this immediately and will do so within seconds if they get into your SQL Server.  If your applications don't need XP_CMDSHELL, and you don't have any third party tools such as backups or monitoring tools that need to use XP_CMDSHELL, you should disable it.  If you do need it, you should make sure it is only open to use by a few accounts.

Developers should architect applications that avoid the need to use XP_CMDSHELL.  In practice, very few applications require the use of XP_CMDSHELL and it is somewhat of a relic of a bygone era.

There are at least a dozen other features than should be disabled if they are not used.  You can find them under the CIS Benchmarks under the topic of Surface Area Reduction.  The [Center for Internet Security](https://www.cisecurity.org/cis-benchmarks/) provides benchmarks for SQL Server and many other products, along with tools to help you insure your environment is managed securely.  Much of their guidance matches what you will find on this web site.

###### SQL Server Features to disable

1. Ad Hoc Distributed Queries
2. clr enabled
3. cross db ownership chaining
4. Database Mail XPs
5. Ole Automation Procedures
6. remote access
7. remote admin connections
8. scan for startup procs

Trustworthy databases



{{< alert theme="danger" dir="ltr" >}} **Disable XP_CMDSHELL if you are not using it.**
{{< /alert >}}