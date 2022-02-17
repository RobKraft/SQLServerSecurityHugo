---
title: "Admin Login Accounts"
description: "Guidance for Administrative Accounts."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 6
---

SQL Server requires an account that allows someone to configure and manage the SQL Server, and that account is called an Admin account.

Admin accounts should not be shared.  Each person should have their own.  Ideally the people with Admin privileges on SQL Server are part of a group in Active Directory that grants the privilege.

* Applications should probably never use an Admin account to connect to SQL Server.
* Some third party SQL Server management tools may require an Admin account to enable their full functionality.  Ideally you can create an Admin account specifically for the tool.
* The 'sa' account should not be used as an Admin account unless it is your only option.

For even stronger security, no user's typical login to the operating system should have Admin privileges on SQL Server.  Instead, people that are considered Administrators should have another login for the operating system that they only use when they need to perform an action only allowed with their Admin credentials.  This practice reduces the capabilities of a hacker that is limited to using the credentials of the logged in user.

{{< alert theme="danger" dir="ltr" >}} **Disable the 'sa' account and never use it!**
{{< /alert >}}
