---
layout: default
title: Stonefield Query 5.0
nav_order: 7
parent: Previous Releases
grand_parent: Home
---

# New Features

* Stonefield Query is now built using ASP.NET Core. The new platform has a number of benefits, including greatly improved loading performance, the ability to self host, and support for additional hosting platforms.

* The Stonefield Query Enterprise installer no longer installs IIS Express since that's no longer needed. When testing a project locally from Stonefield Query Enterprise Studio, the new self-hosting option is used.

* Stonefield Query is now available in 64-bit and 32-bit versions, the latter necessary if you have to connect to a 32-bit data source. By default, the Launch Stonefield Query function in Stonefield Query Studio launches the 64-bit version, but if you want to be prompted for which version to use, turn on the Prompt For 32-bit vs 64-bit setting in the Options page.

* The Refresh dialog has a new Extended Logging option that, if turned on, performs additional diagnostic logging in case issues arise.

* External authentication via Open ID 2.0 is no longer supported, and has been replaced with Open ID Connect instead. In addition, you can also enable external authentication using Google, Twitter, Facebook, and Active Directory Federated Services.

* The Open Project dialog now has a text box so you can type a path if desired.

* If you use the SQL Server ODBC driver to connect to a database, you are now asked if you want to the use SqlClient provider instead, since it works better.

* The Select Table dialog now shows the type of each object: table, view, or "sproc" for stored procedure.

* If a table uses StoredProcedurePlugin as its plugin, you are prompted to refresh the table so the list of fields is correct.

* Added additional logging to various scenarios. 

* A new provider is available for SQLite data sources.

* Field values retrieved from the database are now converted to the type stored in the data dictionary for that field.

* Added better support for field names that begin with a digit.

* A new configuration option is available to skip retrieving the schema for a query.

* You can now specify a complex join that includes additional tables in the join. This is useful if you need to specify a join that must always include a third table, for example.

* User themes are now loaded from an xml file (themes.xml). Add any additional themes to this file to make them available to the end user.

* Stonefield Query now supports encrypted query strings in the URL.

## Bug Fixes

* The help files now contain the correct branded company name and email address.

* A bug that caused an issue with the table name for fields not matching the table name after a table is renamed was fixed.

* A bug that caused the Default Table configuration setting to display a GUID rather than the table name was fixed.

* Fixed an issue with parameters not being sent to a stored procedure properly.

* Fixed an issue with custom logo images not being displayed. 

* Fields with the SByte data type will now have the proper type visible.

* Issues with some types of report conversion were fixed.