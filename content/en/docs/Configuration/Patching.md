---
title: "Patches"
description: "Keep your SQL Server Cumulative Updates (CU) up to date."
date: 2022-02-27T00:36:14+09:00
draft: false
weight: 10
---

###### Patches, known on SQL Server as Cumulative Updates

Update your SQL Server to the latest Cumulative Update (CU) as soon as reasonable after release.  Cumulative Updates often contain fixes to vulnerabilities.  When the world's security defense system is working well, a "good guy" will identify a security vulnerability in a product, such as SQL Server, and let the product vendor (Microsoft) know.  The vendor is then given time, often 30 to 60 days, to provide a fix for the vulnerability before the security "good guy" that discovered the vulnerability makes it known to the public.

This means that when you apply a CU shortly after release you may be fixing vulnerabilities that are soon to be announced to the world.

Often the vulnerability patched is one that would allow a buffer overflow to occur when a specifically crafted request is sent to the SQL Server, and this can be done without needing to log in to SQL Server first.  The buffer overflow vulnerability is complex to explain, but can allow hackers to run their own code on the server and take over the server remotely.

You can receive a notification when new patches are released at this helpful site:
[https://sqlserverbuilds.blogspot.com/](https://sqlserverbuilds.blogspot.com/).

{{< alert theme="danger" dir="ltr" >}} **Update your SQL Server to the latest Cumulative Update (CU) as soon as reasonable after release.**
{{< /alert >}}
