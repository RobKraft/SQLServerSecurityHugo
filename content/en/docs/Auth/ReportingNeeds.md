---
title: "Reporting Needs"
description: "Guidance for configuring accounts used by AdHoc reporting tools."
date: 2022-02-27T00:36:14+09:00
draft: false
weight: 12
---

###### Handling security for users with AdHoc reporting needs

A common scenario for application developers is an application with logic restricting how data can be edited, but some of the people that use the application also need to use adhoc reporting tools to query the data.  I recommend that the application use a login and password, or that it use Integrated Security if it is only a web application running under a non-human account.  Then you can use Integrated Security to provide ReadOnly access for the human users to access SQL Server data through any product.  

If you have desktop applications, and users also have adhoc products that may allow them to bypass the rules coded into your applications, it is difficult to use Integrated Security.  One approach that might work is to restrict the permissions of users connecting through Integrated Security to read only access along with the ability to execute stored procedures.  Perform all data modifications using stored procedures.  This approach prevents most adhoc tools from being able to modify the data, unless they can understand and execute the stored procedures. 

{{< alert theme="danger" dir="ltr" >}} **Disable the 'sa' account and never use it!**
{{< /alert >}}