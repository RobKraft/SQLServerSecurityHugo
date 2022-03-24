---
title: "What is Data in Transit"
description: "A definition of Data in Transit and where it happens related to SQL Server"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 2
---

###### Data in Transit

Data is always considered to be in one of two states:

* Data at rest:  Data that is committed in the database.  Also Backups of databases.
* Data in transit:  Data heading into our out of a database

We need to consider the security concerns regarding the following common scenarios for Data in Transit:

* The connection by a user or application connecting to SQL Server.  Are credentials supplied and are they encrypted to prevent being captured?
* Data sent from applications on internal servers to the SQL Server
* Data sent to applications on internal servers from the SQL Server
* Data sent by client applications and devives to server applications, most typically data sent from web browsers to web servers

{{< alert theme="info" dir="ltr" >}} **Data sent by applications to and from SQL Server is NOT encrypted by default.**
{{< /alert >}}

I need a picture here:

The flow of data between an end user of an application and sql server, in which the web site user is changing their mailing address:

* A person logs in to a web application.  It is important to point out here that the person is not (SHOULD NOT) be using credentials for a connection to SQL Server.  The user should be providing credentials for the application, and these credentials should be managed by an Identity Provider.
* The browser sends the persons "application login" credentials to the Identity Provider via HTTPS and the Identity Provider returns a token that allows the user to continue using the web server application.
* The person on the web site enters their address and clicks a button to send data from the browser client to the web server.
* The browser probably encrypts the data to be sent to the web server if the application is used over the Internet.  This is done via HTTPS (aka TLS 1.2+).  IF the web application is used internally, there is a greater chance that HTTPS is not used, but it probably should be.
* The web server decrypts the HTTPS encrypted information and sends it to the web server application
* The web application places the information in variables in memory
* The web application constructs SQL statements to send to SQL Server
* Connect to SQL Server 
  * The web server application is likely to read a connection string while it is starting up from disk, the registry, a configuration file, or environment variable. That connection string should be securely encrypted if it contains a password used by SQL Authentication.
  * The web server application decrypts the connection string (if necessary) and reads it into the RAM (memory) of the server. (use securestring)
  * The web server application makes a call to the SQL Server for the application to log in to the SQL Server.  The login and password (If SQL Auth is used), are passed as encrypted values.
* After the web server application has connected to SQL Server it sends the SQL statements.  By default, these SQL query is not encrypted as it is sent via the Tabular Data Stream (TDS) protocol from the web server application to the SQL Server, thus a tool like wireshark could sniff and read both the SQL Query and response.
* SQL Server executes the query and returns a response result to the web server application.
  * All of the response data may not be returned immediately.  The client application may pull chunks of it.  But the exact process used does not have any security implications.
* The web server application reads the response from SQL Server into variables in memory.
* The web server application formats a response in a format such as JSON or HTML to send back to the browser client.
* The web server application returns its response to the web server.
* The web server, if using HTTPS, encrypts the response and returns it to the browser client.
* The browser client decrypts the response and renders the HTML in the browser.

If you want to protect data in transit in the scenario about, you need to consider:

* Encrypting the data sent to and from the browser by the web server.  This can be done fairly using using HTTPS, preferably a Certificate Authority (CA) certificate instead of self-signed certificate.
* Protecting data in memory(in RAM), while it is in the memory area used by the web server application.  In .Net, one tools for this is to use SecureString instead of string to store sensitive data.  Although malware sniffing of RAM is rare, it should be considered for applications needing the utmost security.
* Protecting data send to and from the SQL Server from the web server application.  This information is not encrypted by default and can be easily read by a tool such as wireshark.  SQL Server has the ability to encrypt all traffic between the application and the SQL Server for enhanced security.
