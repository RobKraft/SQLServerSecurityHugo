---
title: "AWS/Azure"
description: "Authentication options available in cloud environments."
date: 2022-02-27T00:36:14+09:00
draft: false
weight: 14
---

###### Best Practices for Azure 
In 2022, the best security posture for applications built in Azure is to use 'Active Directory Managed Identity'.  This allows you to define a connection string that you don't have to protect as secret, and it restricts access to your SQL Server database to only those services (such as web applications, Azure functions, and Azure Message Queues) that need the access.  

###### Best Practices for AWS 
Similar to Azure, in AWS you should create execution rules for your services that need to connect to your database and assign permissions to those roles in IAM to allow them to do so.

{{< alert theme="danger" dir="ltr" >}} **Disable the 'sa' account and never use it!**
{{< /alert >}}