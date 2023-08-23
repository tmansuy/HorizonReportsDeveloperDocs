---
layout: default
title: Stonefield Query 3.5
nav_order: 7
parent: Previous Releases
grand_parent: Home
---

# New Features

* Meta data discovery now works with any database with a .NET provider and can handle tables with more than 255 fields. After discovery is complete, a dialog may appear if there were issues that need to be addressed.

* The Help menu has a new Stonefield Query Customer Portal function.

* The new Automatically Query Values When Editing Filter configuration setting determines whether Stonefield Query retrieves the unique values for the field in a filter condition as the user enters a value for the condition.

* If the new URL For Customer Portal configuration setting is filled in, the Help menu in Stonefield Query includes a Customer Portal item that navigates the user's browser to that URL.

* The User Resources panel has settings for Options, Formulas, ChangePassword, and ImportExport, which determine whether users can access those functions in Stonefield Query.

* A new plugin type, ReportPostProcessingPlugin, is available. This plugin can be used to perform any final modifications to the report output just prior to uploading, emailing, or saving the report to a file. 

* The toolbar in Stonefield Query Enterprise Studio now has a Back button that takes you back to the previously selected item. It also has a drop-down list so you can specifically select which item to return to.

* The Prompt for Subtables option was removed from dialogs related to meta data discovery.

* ConnectionStrings.xml has a different structure than in earlier versions.

* Extended diagnostic logging of the meta data discovery process is now only performed when a file named Log.txt exists in the Data subdirectory of the Stonefield Query program folder.

* You can tell Studio not to refresh relationships between tables when refreshing the data dictionary by setting the RefreshRelations setting in Settings.xml to false.

* The version of each plugin being loaded is now logged to the main log file. Stock plugins now have a version number that matches the major release version.

* Support has been improved for having the same table in different databases in the project.

* HTTPS redirection is now done using HSTS, which improves security.

## Bug Fixes

* Captions for fields in MySQL databases are handled better now.

* Connection strings for other .NET providers are now read from ConnectionStrings.xml as the documentation indicates. 

* The LookupFieldConverter builder now adds the database name to table names if there's more than one database in the data dictionary.

* Adding a relation when a collapsed table node is selected no longer causes an error.

* A bug that prevented HelpMapping.xml from being installed was fixed.

* Character values coming from the database are now automatically trimmed of trailing spaces to ensure filter comparisons work the way you expect.

* If a project settings file that doesn't exist is passed as a parameter, the startup process is halted earlier and the reason why is now logged.

* Fixed a logger-related error that would appear when testing a project in IIS Express. 