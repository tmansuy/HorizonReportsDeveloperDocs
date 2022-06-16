---
layout: default
title: Using a Stored Procedure for Data Access
nav_order: 12
parent: How To
---

The report writer normally sends a SQL statement to retrieve records from a database. If you wish to call a stored procedure to retrieve records for a particular table, you must create a virtual table that contains the fields returned by the stored procedure and a virtual table plugin with a Select method that calls the stored procedure when a report containing fields from the virtual table is run. See the [Virtual Table](vfps://Topic/_3QV0SA9WN) plugin for more information and the [Select]({% link _docs/plugins/virtualtable/select.md %}) method for an example.