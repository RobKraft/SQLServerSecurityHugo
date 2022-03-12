---
title: "What is the risk posed by SQL Injection?"
description: "The damage that can be done by SQL Injection"
date: 2020-01-28T00:34:51+09:00
draft: false
weight: 4
---

###### What is the risk posed by SQL Injection?

An application with a SQL Injection vulnerability can allow a hacker to take over all the computers in an organization with malware.  This has occurred on many occassions.  SQL Injection has been used to:

* Retrieve sensitive data from databases,
* Modify data in databases,
* Delete data in databases,
* Create tables in databases,
* Delete entire databases,
* Install malware on the computer running the DBMS and take control of the computer,
* Spread malware to all computers in the company and gain access to all of them.

The damage that a hacker can cause by SQL Injection is determined by the security implemented at multiple levels.

* If the application permissions only allow read access to a database, then information disclosure is the only risk.  However information disclosure means that any information contained with the database can be exposed, including financial data, health data, personal information, and passwords.
* If the application permissions allow data modification, then data may be altered in any way, added, or deleted by SQL Injection.
* Hackers could insert URLs to malicious websites that download malware so that when other users query the data and activate those URLs their own computers are infected.  This technique is referred to as second-order SQL Injection.
* If the application permissions allow database owner permissions then the entire database could be deleted, tables could be created, new stored procedures could be created to replace existing ones.
* If the application permissions allow SQL Server administrative actions, then any alteration could be made to the SQL Server including changing all the logins on the SQL Server, deleting all data in the SQL Server, or altering content in any way.
* Finally, if the application permissions allow access to the underlying operating system, SQL Injection could be used to install malware including Command and Control software that allows hackers to take over the server and other servers in the network.
