---
title: "Protecting Ports"
description: "Guidance for securing protocols and ports."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 2
---

###### Ports and Protocols used by SQL Server

Many people know that the SQL Server service listens on TCP/IP port 1433 by default.  All the automated hacking programs know that most SQL Servers run on port 1433.  Most malware scans look for SQL Server running on port 1433, and if no services are found running there, the automated malware moves on to another server.  This makes running SQL Server on a port other than 1433 one of the simplest changes you can make to reduce the number of hacking attempts your SQL Server is exposed to.

SQL Server can use protocols other than TCP/IP for connections.  You should only enable the protocols you are using.  Protocols should be enabled or disabled using SQL Server Configuration Manager.  The "Shared Memory" protocol is only used by applications running on the same server as the SQL Server service.  You should probably leave that one enabled.  You can probably disable the "Named Pipes" or "VIA" protocols unless you are using them.

{{< alert theme="warning" dir="ltr" >}} **Disable the Named Pipes protocol if you are not using it.**
{{< /alert >}}

You need to pick a TCP/IP port that is not in use by another service.  Also, it is good to avoid picking a port that is used by another common product so that a malware scan for that product does not inadvertently detect your SQL Server is running on that port.  Here is a [list of default port numbers used by products](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers).

Use SQL Server Configuration Manager to specify the port number.

{{< alert theme="danger" dir="ltr" >}} **Configure SQL Server to listen on a non-standard port.**
{{< /alert >}}

Some people will tell you that changing the port number from 1433 is not a good security practice.  They say this because they say port scanners can find SQL Server on any port.  Technically that is true, but in practice, from my own experience, I don't see it happening.  And you can test this for yourself.  Use Azure or AWS and stand up two SQL Servers, one on port 1433 and one on some other port.  Then monitor the failed login attempts for each.  I have clients that use port 1433 and clients that use other ports.  On the SQL Server using port 1433 exposed to the Internet we see attempts to login as 'sa' and other accounts within hours, sometimes within minutes, of bringing the server online.  And within a week we see login attempts on average of one per second for servers running on port 1433.  But the SQL Servers that run on ports other than port 1433 may go a month without a single attempted login by the hackers.  And servers that have been running for years on a non-standard port get only a few attempted logins per month that are malicious attempts.

There are three reasons why you should run SQL Server on a port other than 1433:

* Most hacking is done by automated tools, and most tools will only check port 1433.  It is true that some tools will check other ports, but by using a port other than 1433 you are protecting your SQL Server from being identified by most tools.
* Scanning every port from 0 to 65535 is likely to be noticed by security protocols that a lot of companies use, as well as security defenses deployed by your Internet Service Providers and hosting services.  Therefore few hackers attempt frequent brute force scans of all ports because their source IP address will often quickly get blocked.
* Scanning every port from 0 to 65535 takes time, and one principal of security is that all security defenses are designed to slow down and discourage attackers, not to stop them.  Although we would like to stop them, it is very difficult to stop an attacker that is very dedicated and focused on a single target.  However, every additional piece of security or difference in your system that you put in place slows the attacker down and allows your security defense team more time to detect the attacks and stop them.

Ultimately, any security guidance depends a lot on your environment.

* If your SQL Server is exposed to the Internet, you should probably change the default port number.
* If your SQL Server is internal, and the date it contains is not extremely sensitive, then the costs of changing the default port number may outweigh the benefits.
* If your SQL Server is internal, and the date it contains is extremely sensitive, then you should probably consider changing the default port number to slow down attackers that have gotten into your internal network.

Further Reading:

* Information about [other ports used by SQL Server products](https://www.sqlsplus.com/sql-server-ports-tcp-and-udp-ports/) including 1434, 2383, 2382, 135, 80, and 443.
* Microsoft recommends that you [disable netbios and SMB ports](https://docs.microsoft.com/en-us/sql/sql-server/install/security-considerations-for-a-sql-server-installation?view=sql-server-ver15) on a server running SQL Server