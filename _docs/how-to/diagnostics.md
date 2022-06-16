---
layout: default
title: Getting Application Logs
nav_order: 7
parent: How To
---

Horizon Reports has built-in "diagnostic" logs that can be helpful for determining the cause of errors or other problems. Information about each stage of application startup, setup, database connection, report runs, and shutdown is logged to a file called AppLog.txt in the Logs subdirectory of the SQWeb folder. If the information in these files doesn't help you track down the problem, contact [Horizon Reports Technical Support]({% link _docs/support.md %}); we can likely help you track it down. If you don't have access to the web server to retrieve the log file, use the Download Application Log function in the Tools menu.

There are also several filtered logs that contain more specific information: 

* *crashdump.txt*: If a low level error occurs during startup that can't be handled, it will be logged in this file.

* *reportlog.txt*: This log contains log events specifically from the report engine. For example, each time a user runs a report, it will be logged here. 

* *schedulelog.txt*: This log contains log events specifically from the scheduler. 

* *serverlog.txt*: This file contains a log of all HTTP requests to the server.