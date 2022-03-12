---
title: "Where to protect sensitive data"
description: "Where does sensitive data need to be protected in SQL Server?"
date: 2020-01-28T00:34:51+09:00
draft: false
weight: 4
---

###### Where is the sensitive data?

Sensitive data needs to be protected at all times.  To learn about protecting sensitve data in transit follow [this link](/docs/transit/transit/).

We will consider everything else to be 'sensitive data at rest'.

Here are places where we have 'data at rest':

* Data that is committed in the database.
* Data in transaction logs not yet committed to the database.
* Backups of databases.
* Data in SQL Server log files.
* Data in Web Server log files.
* Data in other log files including Windows Event Viewer and application logs.
* Data displayed in application, or sent by applications to reports and emails and other environments.
* Data shown in third-party reporting tools or pulled into data warehouses.
* Data in all the same areas as above but in non-production environments.
