---
title: "What is SQL Injection"
description: "A description of SQL Injection"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 2
---

###### What is SQL Injection?
SQL Injection is a technique for hacking software applications by passing values to an application that construct SQL commands to do things the application developers did not intend.  Many applications read and write data to/from relational databases, and the language used by most applications to talk to relational databases is SQL.

SQL Injection is very easy to exploit when application code fails to account for the risk.

###### A basic example of SQL Injection
A user enters their email address into a web page to log in.
The application code constructs a query in the SQL language to look for the user in the database.  The command to code to construct the SQL looks something like this:

```
declare sqlstmt as string
sqlstmt = "Select * from people where email = '" + logonEntered + "'"
```
Assuming the value for logonEntered is an expected value like RobKraft@myemail.com, the SQL statement sent to the database will look like:
```
Select * from people where email = 'RobKraft@myemail.com'
```
But that bit of code is vulnerable to SQL Injection, so a hacker could enter a value like the following in the log in field on the web page:
```
' or AdminAccount=1 --
```
Causing the SQL command sent to the database to look like this:
```
Select * from people where email = '' or AdminAccount=1 --'
```
In the above example, the query will now return all the accounts that are for administrators.  The two dashes at the end tell the database engine that the rest of the command sent to the database is just a comment.

***
---

**Examples to come**