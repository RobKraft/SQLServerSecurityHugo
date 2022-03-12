---
title: "What types of data are sensitive"
description: "A definition of the types of data considered sensitive"
date: 2020-01-28T00:34:51+09:00
draft: false
weight: 2
---

###### Types of Sensitive Data

You need to consider many different forms of data related to SQL Server when you consider what you need to protect.

* SQL Login credentials for people.
* SQL Login credentials for applications
* OS Login credentials SQL Server uses to log in to the Operating System
* Personal information such as a social security number
* Credit card numbers and other financial information
* Health care data of individuals
* Company secrets
* Security secrets of other applications such as login credentials
* Personally Identifiable Information (PII) which includes email addresses, phone numbers, and addresses

###### SQL Login credentials for people

It is best to use Windows Authentication and roles within SQL Server to allow most people to connect to SQL Server. Hopefully the only people that might need a SQL Server login are SQL Server administrators.  Even then, it is best not to share SQL Server logins.  The 'sa' account should never be used; but if you create other SQL Server administrator accounts, they should not be used by multiple people.  Each person should have their own account for logging onto SQL Server in an administrative capacity.  Using shared accounts is discouraged for any product.

###### SQL Login credentials for applications

Most applications use the same connection string for everyone using the application.  When the connection string uses SQL Authentication it contains a password and therefore the connection string should be encyrpted.

###### OS Login credentials SQL Server uses to log in to the Operating System

SQL Server needs to log in to the operating system when the service starts running.  Securing the password for this account is easy if you can use a virtual account managed by active directory, but if not the operating system can securely store that password when you enter it manually.  

###### Personal information such as a social security number

Many applications store sensitive information about individuals such as their social security number or other government issued identifier.  This information needs to be protected from exposure to hackers, but also to most people within the company holding the data except for individuals with clearance to see the data, and even then, possibly only in specific circumstances.

###### Credit card numbers and other financial information

When you store this type of information, it needs to be encrypted.  For most businesses, the best strategy is to avoid storing information if you don't absolutely need it.  Another common approach is to outsource the storage of sensitive data, and thus outsource the risks associated with it, by using a third party product to process that information.

###### Health care data of individuals

Most information related to a person's health and related payment systems has been deemed sensitive and needs to be stored securely.

###### Company secrets

Many companies have internal trade secrets and financial information that they don't want known publicly.

###### Security secrets of other applications such as login credentials

Databases are often used to store the credentials of users for other applications.  Today, if you are designing a new solution to store secret credentials and keys it is probably better to use a data store specialized in storing such secrets.  A key vault.

###### Personally Identifiable Information (PII) which includes email addresses, phone numbers, and addresses

PII is listed separately from the items above because it was only in the decade of 2010 that organizations began protecting this information more strongly and some government added regulations to do so.  PII data can include basic information about people such as their email address and mailing address and phone number.  Yet those pieces of information need to be accessed and used frequently by applications, unlike a social security number, therefore secure storage of PII data and restricting its full display is usually more challenging than protecting a single, rarely used value, such as a social security number.
