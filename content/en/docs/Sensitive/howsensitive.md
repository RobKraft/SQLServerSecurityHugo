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

Transparent Data Encryption (TDE) is a feature offered in SQL Server that encrypts your entire database.  But it is not the answer to all your security concerns.  In fact, the primary benefit of implementing TDE is that if someone steals your hard drive, they won't be able to use the database from that hard drive on another computer.  In addition, backups are TDE encrypted so they also cannot be used on another computer with the decryption keys.
TDE helps some organizations comply with regulations.
TDE is available in the Enterprise Edition of SQL Server.  It is also now available in the Standard Edition with SQL Server 2019.
Implementing TDE does not impact your applications at all.  No changes are need to your code or connection strings.

###### Protecting exposure of sensitive data from viewing by some application users

Many applications need to encrypt or protect some sensitive information from some users, but allow it to other users, or just in some cases.  There is rarely an easy solution.  Here are some considerations.

1. Don't store the sensitive data!
The best approach you can take to sensitive data is to not store it at all.  Outsource the risk of storing sensitive data to a third party provider.
2. Passwords
Use an external product for passwords.  Don't store them in your SQL Server database.  See this article.
If you feel you must store passwords, you should store them as hashes, not as something that can be decrypted.  See this article
3. Credit card numbers
Use an external product for credit cards.  Don't persist them in the database if the application is just passing them through to another application.
Consider integrating your application with a third party payment solution that handles payments and takes all the related risk of securely managing credit cards.
You could consider storing them in an secrets management product such as [HashiCorp's Vault](https://www.vaultproject.io/) if used on-premise.  But it would be even better to use [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) or [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/) if you are in one of those clouds.

##### When you need to store encrypted data
When you have data that you need to store securely in your database you have these options:

* Allow the application to encrypt and decrypt the data.  SQL Server does not need to be involved other than to store the data, probably in varbinary data types.  This makes it easy for SQL Server, but it means that adhoc reporting tools are unable to read the encrypted data.  The application(s) that read and write the data need to securely manage the encryption keys for doing so, and those keys need to be installed on every computer where this will be done.  Here is an article:
* Encrypt/Decrypt a column contents using [SQL Server's EncryptByKey and DecryptByKey](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/encrypt-a-column-of-data?view=sql-server-ver15).  This requires use of these built-in SQL Server functions every time those columns are accessed?  And what about where clauses on them?
* [SQL Servers's Always encrypted](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine?view=sql-server-ver15).  

However, since SQL Server isn’t doing the encrypting, many functions won’t work with this approach. In particular, you can’t sort, index, look for string fragments or do calculations on data that’s encrypted.

Here is Microsoft's guidance on [SQL Server's Encryption options](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption)

[Dynamic Data Masking](https://docs.microsoft.com/en-us/sql/relational-databases/security/dynamic-data-masking?view=sql-server-ver15)
https://medium.com/poka-techblog/the-best-way-to-store-secrets-in-your-app-is-not-to-store-secrets-in-your-app-308a6807d3ed

  If you collect credit card numbers,
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