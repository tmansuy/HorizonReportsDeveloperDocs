---
layout: default
title: Stonefield Query 4.0
nav_order: 5
parent: Previous Releases
grand_parent: Home
---

# New Features

* A new plugin interface type, IStonefieldQueryLinkActionPlugin, is available. This plugin allows you to create custom events to be executed when a user clicks a field in a report.

* You can now use your own Open ID Authentication server and bypass Stonefield Query authentication. New configuration settings (Open ID Authentication OP Identifier and Log Off Redirect URL) are available to enable this.

* Logging has been improved in many places.

* A new configuration setting allows you to add "with nolock" to table elements in a SQL query (SQL Server only).

* The new Allow Password Resets configuration setting allows you to determine whether to allow a user to request a password reset email in case they forget their password.

* If you use Stonefield Query inside an IFrame, you can subscribe to a new "bootstrapperDone" event with addEventListener. This event fires when once loading is finished.

* You can now include files called "custom.js" and "custom.css" in your project folder. These files can contain any custom JavaScript or CSS that you want loaded when the Stonefield Query loads.

* A new API route is available in Stonefield Query for generating a user token.

* The View Table Contents function has much better performance than before and no longer has data type issues with certain tables.

## Bug Fixes

* Fixed an issue with the View Table Contents function not working properly for certain database engines.

* The View Table Contents function now handles the parameter data type when prompting you for values for virtual tables for stored procedures.

* The plugin edit button now handles the case where there's more than one solution and the case where there's an empty solution in the source folder.

* The SQL Statement plugin builder now handles the data type of parameters properly and encodes the SQL since it may contain characters that aren't legal in XML.

* The Publish function handles failure to upload files in the x86 and x64 folders better. It also uses the new Publish folder as the source of the files to publish so avoid issues with files Studio has open.

* Studio now handles the stored path for the last open project better to avoid an issue in which it didn't always open the last project at startup.

* Studio now uses ".dat" as the extension for the SQLite database if it isn't specified.

* Connections strings are now encrypted in the diagnostic log file.

* A bug that caused an error when adding or refreshing a database and the Add All Tables to Data Dictionary option is turned off was fixed.

* A bug that caused a table removed from the selected list in the Select Tables dialog from appearing in the available list was fixed.

* The correct URL is now used when you click the Videos link in the Studio Start Page.

* Studio now saves any changes you made to any settings before publishing a project.