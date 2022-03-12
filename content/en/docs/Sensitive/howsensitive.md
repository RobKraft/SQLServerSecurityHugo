---
title: "How to protect sensitive data"
description: "Howw can we protect data?"
date: 2020-01-28T00:34:51+09:00
draft: false
weight: 6
---

###### What tools do we have to protect sensitive data?

Sensitive data can rest in a number of different places, and the tools and methods we use to protect that data varies based on the area.

Unfortunately, most people probably need to learn and configure multiple features to protect data in all the ways it needs to be protected.  You might be able to use TDE to encrypt an entire database, but that does not protect the credit card numbers in the database from being displayed to legitimate users of the application.  We need to consider each use case, and the tools for each case.

###### Protecting against a backup of the database from getting restored on another server

TDE

###### Protecting exposure of sensitive data from viewing by some application users

App encryption.  SQL Encryption.  Masking.  Structural encyprtion?
Partial reveals. How to show non-encrypted data to some people when needed
-impact on 3rd party tools

###### Protecting data in non-production systems

###### Protecting data in database backups

###### Protecting data in log files


* On screen and reports
* In server memory, application memory
* On disk

* Data that is committed in the database.
* Data in transaction logs not yet committed to the database.
* Backups of databases.
* Data in SQL Server log files.
* Data in Web Server log files.
* Data in other log files including Windows Event Viewer and application logs.
* Data displayed in application, or sent by applications to reports and emails and other environments.
* Data shown in third-party reporting tools or pulled into data warehouses.
* Data in all the same areas as above but in non-production environments.