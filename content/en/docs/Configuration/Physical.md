---
title: "Physical Security"
description: "Guidance for physical security of SQL Server."
date: 2020-01-28T00:36:14+09:00
draft: false
weight: 2
---

###### Secure the physical environment

Thieves may steal servers.  In most cases, they probably don't know what the servers contain and may plan to simply wipe the hard drives and resell the hardware.  In some cases, they may target your organization in order to obtain information they believe is on a server or hard drive.

{{< alert theme="info" dir="ltr" >}} **Keep server hardware with sensitive data behind securely locked doors.**
{{< /alert >}}

If your data is sensitive enough to require security it certainly also needs to be backed up regularly, and ideally the backups go to an offsite location.  

{{< alert theme="info" dir="ltr" >}} **Keep backup medium and/or servers containing backup files of databases with sensitive data behind securely locked doors.**
{{< /alert >}}

###### Dealing with hosting services

Many organizations use Internet Server Provider(ISP), co-location server facilities, and Cloud Service Providers to host servers that contain databases.  Do you trust that the physical security provided by your server host is sufficient to protect your data from physical theft?  Do they have good security controls, processes, and auditing to track the people entering the facility?  Can they provide you documentation of their security processes?

If you are backing up your data to a backup provider at your ISP or cloud host, are you confident the servers at the backup location, and all the locations the backups may be replicated to, are physically secure?

###### Dealing with sensitive data on laptops

Some systems install SQL Server on laptops and other portable devices and allow sensitive data to be stored within them.

* Consider installing software on those devices so that they can be ["remotely wiped"](https://www.bing.com/search?q=remotely+wipe+laptop) if necessary.
* Consider requiring the use of biometrics such as fingerprints or retinal scans to unlock the device for use.
* Consider using technologies like [bitlocker](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-overview) that require a person to enter a pin or connect a USB Key device in order to use the computer.
