---
title: "How to Prevent SQL Injection"
description: "Practices to reduce the risk of SQL Injection attacks"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 6
---

Many of the actions described on this web site will help you mitigate SQL Injection attacks.  The most important and useful mitigation tool is for the application developers to use the tools of the programming language to mitigate and possibly eliminate the risks of SQL Injection.

The precise steps a programming language should take to prevent SQL Injection depends on the programming language and the DBMS as well as some DBMS configurations.  The example below is at risk for SQL Injection:
```
declare sqlstmt as string
sqlstmt = "Select * from people where email = '" + logonEntered + "'"
```
The correct code should replace any single quotes passed in as data with two single quotes.  Something like this:
```
declare sqlstmt as string
logonEntered = Replace(logonEntered, "'", "''")
sqlstmt = "Select * from people where email = '" + logonEntered + "'"
```
Handling single quotes in the manner shown above is not sufficient to prevent all forms of SQL Injection.  See this article for examples of all SQL Injection forms and how to prevent them in a .Net language.
TODO

Programmers are not the only ones responsible for mitigating the risk of SQL Injection.  Given the prevalence of use of third party programming libraries as well as the possibility of human error, developers should not carry the full burden of reducing the risk of SQL Injection.  Any strategy to reduce hacking risks should rely on multiple layers of security to slow hackers down.

The following activities also help mitigate SQL Injection risks:

* Have SQL Server log in to the operating system with the least privileges needed.
* Have applications use only the db_datareader and db_datawriter roles.  Do not allow applications to create tables or other objects in databases.
* Disable xp_cmdshell
* Monitor Logs
* Add a Web Application Firewall (WAF) that can scan for SQL Injection risks

*links to tools to help write better code*