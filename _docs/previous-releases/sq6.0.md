---
layout: default
title: Stonefield Query 6.0
<<<<<<< Updated upstream
nav_order: 3
=======
<<<<<<< Updated upstream
nav_order: 2
=======
nav_order: 4
>>>>>>> Stashed changes
>>>>>>> Stashed changes
parent: Previous Releases
grand_parent: Home
---

# New Features

* Stonefield Query is now built using ASP.NET Core 5.0. This version supports hosting the web application in an IIS Process, where the previous version required the use of a proxy. This should improve performance. If you're migrating from a previous version, see the Migrating from an earlier release topic.

* Stonefield Query can now automatically compile your plugins for you.

* A new plugin type, StonefieldQueryCustomReportOutput, allows you to specify a custom output type. By default, Stonefield Query can email a report or upload it to an FTP site. This plugin allows you to specify a new type, like uploading to Azure, or storing in a local document database, for example.

* A new log file is available, "reportlog.txt". This log file contains a log of which reports were run, when they were run, and how long each took to run.

* Stonefield Query now supports running in a Web Farm.

* Stonefield Query no longer uses the Windows scheduler to execute schedules. They now run in process, which means there's a lot less overhead involved in starting a schedule. This also allows the scheduler to take advantage of load balancing when running in a Web Farm.

* You can now use UNC network paths in a provider connection string (i.e //servername/sharename).

* Improved startup performance.

* Users with 2FA enabled are now redirected to an intermediate token page, rather than relying on javascript on the login page to support this.

## Bug Fixes

* Improved logging in multiple areas.

* Fixed several issues with error handling.

* Fixed a bug with FTP server settings being stored in plain text (they are now encrypted).