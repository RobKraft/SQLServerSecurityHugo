---
title: "Operating System"
description: "Secure the Operating System"
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 4
---

###### Operating System Security

SQL Server can run on Windows or Linux.  Regardless of which operating system you use, the follow rules apply:

* Run SQL Server only on supported versions of the operating system.  Don't run SQL Server on old versions of the operating system that are no longer supported.
* Apply patches and updates, especially security patches, to the servers as soon as reasonable to reduce the risk a server exploit allows access to your SQL Server.
* Eliminate or minimize the use of other services on your server.  To minimize the risk a vulnerability in one product leads to explotation of other products, security guidances always recommend dedicating servers to a single product or service.  This is very practicle now that virtual machines and containers are ubiquitous.  Don't run a web server, or Exchange server, or even an FTP server on a server running SQL Server.  Run only the minimal services required for the SQL Server service.
* Microsoft recommends that you [disable netbios and SMB ports](https://docs.microsoft.com/en-us/sql/sql-server/install/security-considerations-for-a-sql-server-installation?view=sql-server-ver15) on a server running SQL Server.
* If you use several services that Microsoft provides with the SQL Server product (SSIS, SSRS, etc.), consider running each on separate servers.
* Ensure the firewall on your operating system is running and has only the necessary ports open.

Windows Server [End of Life dates](https://endoflife.software/operating-systems/windows/windows-server)

###### Secure SQL Server files

The hard drives of servers are often accessible to people on the same network using Windows File Explorer and other tools.  Ideally, such access should be restricted and limited for any files on a server running SQL Server.  It is not impossible for a hacker with sufficient access to replace one of the files installed as part of the SQL Server product with a malware infected version of the file that appears to operate normally but allows the hacker access to modify or steal sensitive information.

[System File Checker](https://docs.microsoft.com/en-us/troubleshoot/windows-server/deployment/system-file-checker) may be able to identify files that have been replaced with malware versions.

It may be useful to allow personnel read-only access to some files and folders managed by SQL Server to view logs and monitor disk space usage, but be aware that hackers may also be able to access that data from other computers if the security to those files is not well protected.
