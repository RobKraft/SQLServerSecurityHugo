---
title: "How to protect Data in Transit"
description: "Guidelines for protecting Data in Transit"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 4
---

###### How to protect data in transit

We have different tools to consider for protecting the different types of data in transit.

* The connection by a user or application connecting to SQL Server.  Are credentials supplied and are they encrypted to prevent being captured?
  * [How to encrypt connection strings in .Net application](https://www.c-sharpcorner.com/article/encrypt-and-decrypt-connectionstring-in-web-config-file/)
* Data sent between applications on internal servers and SQL Server
  * [How to encrypt data between applications and SQL Server](https://www.gethynellis.com/2021/01/how-do-i-encrypt-my-sql-server-connections.html)
* Data sent by browser applications and other devices to web erver applications, most typically data sent from web browsers to web servers.
  * Traffic sent over HTTP should be encrypted using HTTPS, also knows as TLS.

