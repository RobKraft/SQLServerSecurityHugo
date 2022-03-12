---
title: "Is SQL Auth Secure?"
description: "Why SQL Authentication is less secure than Windows Authentication."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 15
---

###### Why Microsoft recommends Windows Authentication over SQL Authentication

Microsoft recommends that you use Windows Authentication instead of SQL Authentication whenever possible.  Windows Authentication is more secure because the operating system handles the connection and can use the Kerberos protocol.  Additionally, Windows Active Directory allows more sophisticated password policies and auditing of logins.  Finally, database administrators can't turn off or alter the password policies.

When a SQL Server client first connects to a SQL Server, the Login attempt which includes the password IS encrypted by TLS.  However, it is theoritically possible to intercept that Login attempt with a Man-in-the-middle attack.  The liklihood of this is low, but should be considered for environments that need the most security possible.

Regardless of whether the login uses SQL Authentication or Windows Authentication, [the majority of the traffic to and from SQL Server is not encrypted by default](/docs/transit/transit).

Further reading:

* [This article](https://security.stackexchange.com/questions/245979/how-is-tds-authentication-data-protected) provides a little more info about the Login.
* [SQL Authentication risks](https://www.sqlservercentral.com/articles/can-we-please-stop-sending-passwords-over-the-wire)
* [How to encrypt data between applications and SQL Server](https://www.gethynellis.com/2021/01/how-do-i-encrypt-my-sql-server-connections.html)

#### Will Microsoft make SQL Authentication more secure?
I'll make an educated guess about why Microsoft will not make SQL Auth more secure.  First, the design for SQL Authentication probably originated with Sybase in the early 1990s.  It was not a bad design pre-Internet.  It has been improved to support TLS since those early days.

Second, an OAuth type implementation, as suggested, requires another server and a lot of complexity be added to the product.  I would recommend that Microsoft consider that approach as a third option for authentication, not as a replacement to SQL Authentication.

Microsoft desires backward support for SQL Server and all the community products that use it.  Changing the way SQL Authentication works, even adding a third option, risks breaking products that have co-existed with SQL Server for decades.

The OAuth approach requires integration with an Identity and Access Management system and a Secure Token Server.  Either Microsoft re-invents that wheel and creates a new IAM to install with SQL Server, or allows SQL Server Admins to integrate with an existing one.  Of course either approach entails a lot of risks and potential problems for a product that has been very stable for decades.

Ultimately, Microsoft already provides Windows Authentication, which uses more robust security and an external IAM (Active Directory) for authentication.  So if SQL Server Admins don't feel secure with SQL Authentication, they don't need to use it.  In fact, Microsoft has it disabled by default and Microsoft recommends using Windows Authentication.

Given that Windows Authentication is already the recommended and default option, I doubt Microsoft will ever work to change SQL Authentication.