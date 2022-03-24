---
title: ".Net Code"
description: ".Net Code to Prevent SQL Injection"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 8
---

###### SQL Injection Exploits

SQL Injection exploits can be grouped into three categories.  Once a hacker has detected a SQL Injection, they may use it in any or all of these four ways:

* Send a command and see the result (sometimes called In-Band SQLi or Classic SQLi)
* Send a command and infer the result (Inferential SQLI)
* Send a command that goes through the DBMS (SQL Server) to affect other services such as the operating system (Out-Of-Band SQLI)
* Send a command to insert or modify a database record that contains a SQLi command that will affect other users (Second Order SQL Injection)
You can read more about the first three ways in [this article](https://dzone.com/articles/sqli-part-3-in-band-and-inferential-sqli).  And you can read about second order SQLi in [this article](https://www.sqlservercentral.com/blogs/how-to-steal-data-using-second-order-sql-injection-attacks)

All of the above four ways rely on the same flaws within the application code.  

{{< alert theme="danger" dir="ltr" >}} **ANY of these flaws allows an attacker to craft and run ANY SQL statement they want.**
{{< /alert >}}

Let's cover those vulnerabilities:

###### 1. Mismatched quotes

```
logonEntered = "  ' or 1 = 1--"
sqlstmt = "Select * from people where email = '" + logonEntered + "'"
```

This vulnerability can be stopped by using parameters when passing values for variables in query construction.  It may be possible to replace all single quotes with two single quotes in your application code to fix this.  If you dynamically construct part of the sql such as order by clauses, then this is not an option.  See considerations here:

###### 2. OR clauses

```
id = "3 OR id > 0"
sqlstmt = "Select * from people where id = " + id + 
```
Developers sometimes overlook the SQL Injection risk of numeric fields, but when a numeric field is treated as a string in code until it is passed to the database, it opens the door for attacks by SQL Injection.
The best thing to do is to validate all inputs to your application.  This should be done before you construct the SQL, but it is best to validate the inputs as soon as the application code receives them, which could be in the REST layer or ASP.Net web page of an application.  Validate both data type and length.
See this for some examples:

###### 3. UNION clauses

```
id = "3 UNION Select logon,password from users"
sqlstmt = "Select first,last from people where id = " + id + 
```
You can mitigate this risk the same way as #2.  The point here is that developers need to be aware that SQL Injection comes from techniques other than just the mismatched single quote.

###### 4. Stacking statements

```
id = "3;DELETE * FROM PEOPLE;"
sqlstmt = "Select * from people where id = " + id + 
```
You can mitigate this risk the same way as #1 and #2.  Also by preventing the use of a semicolon in the SQL.  A robust SQL Injection blocker example is here:

###### 5. If statements for discovery

```
logonEntered = " ';  declare @a int select @a= count(*) from sys.databases where name like 'a%' if (@a>0) select 'true' else select 'false'--"
sqlstmt = "Select HasManagerPerms from people where email = '" + logonEntered + "'"
```
You can mitigate this risk the same way as #1 and #2.  The important thing to notice about this attack is that hackers can use it to learn information about your data even when they can't see the direct response of their query.  They may be able to produce a different response in the UI.  In the example, perhaps the website shows different information or enables some fields when a person that is a manager is logged in.  The hacker can look for the fields only enabled for a manager.  Therefore, the hacker can basically ask yes/no questions in your database and assign a yes/no response based on those fields being enabled.

###### 6. Time-based statements for discovery

```
logonEntered = " '; if (select user)= 'dbo' waitfor delay '0:0:10'"
sqlstmt = "Select name from people where email = '" + logonEntered + "'"
```
You can mitigate this risk the same way as #1 and #2.  This attack, like #5, is used when the hacker can't see any response to their attack, but perhaps that can measure how long it takes a web page to be displayed back to them.  By delaying the response, they can, just like in #5, ask the database yes/no questions and determine the answer based on the length of the delay.

###### SQL Injection Attacks are Automated
When you see examples of SQL Injection, you may believe that it would be very tedious for a hacker to learn about your database by running one query at a time and waiting for results.  That belief is correct, but you need to know that hackers used programs to do their work.  There are a lot of programs available that make it easy for a hacker to run thousands of queries against a vulnerable application to discover information in the database.  Most of the SQL Injection hacking is done by automated programs.

###### General Steps To Mitigate SQL Injection Risk

* Validate input to the application.  Make sure the input is of the correct data types and of the expected length before putting it into an SQL statement.
* Use parameters.  Most application frameworks have classes such as ADO.Net to simplify database calls, and the parameters in those frameworks can substantially reduce the risk of SQL Injection.
* Use stored procedures.  Stored procedures do not guarantee that SQL Injection can't occur.  ... Perms on  - especially for mods
* Make it easy for developers to encode strings and dates if they don't always use parameters. To do so... 
* Use a Web Application Firewall.  This is not guaranteed to catch all SQL Injection attempts, but can help.  More about slow attacks and detecting attacks...

###### All applications that communicate with a database are a risk for SQL Injection

WEb apps
REST APIs
Desktop Apps
Imports interfaces

###### .Net Code to prevent SQL Injection

Data input fields, but also URLs and REST APIS. Body content of posts and browser headers.






* [Simple example of UNION and also of Second Order Injection](https://portswigger.net/web-security/sql-injection)
* [For PHP](https://www.ptsecurity.com/ww-en/analytics/knowledge-base/how-to-prevent-sql-injection-attacks/)
* [OWASP](https://owasp.org/www-community/attacks/SQL_Injection)
* [Blind SQL Injection](https://owasp.org/www-community/attacks/Blind_SQL_Injection)
[Troy Hunt on SQLI](https://www.troyhunt.com/everything-you-wanted-to-know-about-sql/)
[Article about approaches to deducing data in web apps](https://www.blackhat.com/presentations/bh-usa-04/bh-us-04-hotchkies/bh-us-04-hotchkies.pdf)
[More detailed attack examples](https://www.invicti.com/blog/web-securtity/sql-injection-cheat-sheet/)