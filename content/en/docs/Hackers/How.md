---
title: "How do hackers attack?"
description: "Describes how hackers are attacking your SQL Servers."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 4
---

###### How do hackers attack my SQL Server?

So, how exactly are hackers going to attack your SQL Server?  Isn't it totally safe behind firewalls and network subnets to prevent any hacks?  The answer is "No!", but firewalls and network subnets help a lot.

###### What are the risks for my SQL Server if it is not exposed to the Internet?

* The major risk for SQL Servers not connected to the Internet usually comes from the risk of SQL Injection via web applications exposed to the Internet.
* Another significant risk for SQL Servers not connected to the Internet is when hackers connect to an internal network via other vulnerabilities not related to SQL Server, and discover a defenseless SQL Server that is easy to attack and exploit.
* A minor risk is that a configuration changes to allow SQL Server to be exposed to the Internet.  It could be done by accident, or it could be done intentionally with the expectation the configuration will be reverted; but then the reversion is forgotten and SQL Server is left exposed.
* Another risk is that a backup of a SQL Server database is placed in a directory exposed to the Internet.  You can find many stories of this happening, not specifically with SQL Server databases, but with many different DBMS products.
* One last risk to consider, is that sensitive data can be stolen in transit to/from the SQL Server.  After all, it is not really usually the SQL Server databases that we want to protect, it is the data they contain, so we need to take steps to insure that data in transit is secured.

###### What are the risks for my SQL Server if it is exposed to the Internet?

* All of the above, of course.  Including the following:
* Many hackers continuously look for SQL Server running on port 1433.  Once detected, they will bombard it with attempts to login as 'sa' and other accounts.
* Hackers on the Internet will look for SQL Server on other ports also, but they often avoid scanning too many ports because it can lead to their detection which can result in their source IP addresses getting blocked.
* If the SQL Server listening process is vulnerable to any known buffer overflow attacks, this knowledge will be built into the hacking software and they will attempt to exploit it.  For example, here is a known [buffer overflow for SQL Server 2000](https://www.fortiguard.com/encyclopedia/ips/11717/ms-sql-server-buffer-overflow).

###### What will hackers try if they have infiltrated our internal network?

If hackers are inside your company network, they will often attempt to move quietly and deliberatly to avoid detection.  This allows them more time to discover more about the network in an attempt to find the most valuable data.  In other cases they will move quickly hoping they can get what they want before being disconnected and removed.

Some of the activities will be"
* All of the above, of course.  Including the following:
* Scanning hard drives for .config files that may contain connection strings for SQL Servers.  They don't scan just .config files, but their first pass scans will often start their looking for the easy and quick vulnerabilities.
* They will scan computers on port 1433 looking for SQL Server.  If they find none, they may or may not look for SQL Server on other ports.  Scanning all ports increases the risk their hacking activities will be discovered.
* Scanning hard drives for application source code that may contain hard coded connection strings.
* Scanning for SQL Server log files.
* Scanning for application log files that may be recording SQL Server other other logon credentials or sensitive data.
* Scanning for backups of the database.  These are often found in known locations, unencrypted, and easy to copy and steal and load on their own SQL Servers.


Github Finding connection strings
Pinging port 1433 (and other ports)
Reading logs
Stealing backups
Stealing data in transit
buffer Overflow
 
Running encryption TLS to talk to command and control