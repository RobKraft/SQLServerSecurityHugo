---
title: "Backup Files"
description: "Guidance for protecting backup files."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 6
---

###### Consider encrypting your database backups

If your database contains no sensitive data that should be protected, then you probably don't need to encrypt the backups of your database.  But keep in mind that even the names, addresses, phone numbers, and email addresses of real people are considered Personally Identifiable Information (PII) and should be protected.

Hackers often search for database backup files that are unencrypted.  They can easily restore the files in their own environments and access all the data they contain.  Therefore it is important to implement encryption as part of your backup process to prevent unwanted theft of data from a file backup that was exposed on the Internet or on someone's personal computer or USB drive.

Every edition of SQL Server since SQL Server version 2014, even the free SQLExpress version, supports encrypting backups.

Many companies use third party tools to backup SQL Server databases on premise.  A good tool will support encryption.

For more information about how to encrypt your database backups, see the [documentation provided by Microsoft.](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/backup-encryption)

