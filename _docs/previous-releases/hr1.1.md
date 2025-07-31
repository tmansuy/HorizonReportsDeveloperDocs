---
layout: default
title: Horizon Reports 1.1
nav_order: 3
parent: Previous Releases
grand_parent: Home
---

# Version 1.1

* You can now customize the name of the [cookie]({% link _docs/how-to/configuring.md %}) that Horizon Reports sends to the browser.

* When [refreshing the data dictionary]({% link _docs/studio/datadictionary/refreshing.md %}), you can now choose specific tables to refresh from a list. 

* The [database tree view]({% link _docs/studio/datadictionary/database-properties.md %}) will now scroll to the previously selected item after a change.

* If you launch Horizon Reports with no [project]({% link _docs/studio/creating-a-project.md %}) created, you are now automatically prompted to create a new project.

* You can now highlight items in the [database tree view]({% link _docs/studio/datadictionary/database-properties.md %}) by last updated date or keyword search.

* Added [Format]({% link _docs/studio/datadictionary/field-properties.md %}) presets for different data types.

* In Studio, you can now right-click on a table and choose [View Table Contents]({% link _docs/studio/datadictionary/view-table-contents.md %}) to retrieve and view the table.

* Added a [connection string builder]({% link _docs/studio/datadictionary/connection-string-builder.md %}) to Studio to help creating database connection strings.

* You can now test [relations]({% link _docs/studio/datadictionary/relation-properties.md %}) with a new Test button.

* The [BeforeExportReport]({% link _docs/plugins/reportengine/beforeexportreport.md %}) plugin method now supports changes to the export options for the report. 

* Moved the default location for [hrsettings.json]({% link _docs/how-to/configuring.md %}) file to Project_Data. This allows setting the file permissions for the application root folder to read-only. Previous installations that have hrsettings.json in the application root will still continue to work normally. 

* Added support for string concat (\|\|) operator when reporting against a data source that requires it (like SQLite).

* Added new URL for [directly exporting a report]({% link _docs/how-to/usingfromotherwebapps.md %}) to file. 

## Bug Fixes

* Fixed a bug where the Studio app wouldn't work properly when hosted from a virtual directory.

* Fixed a bug with custom favicon and logo handling. 

* Fixed an issue using a MySql backend to host the data dictionary database. 

* Fixed an issue with views not being handled properly during a refresh.

* Last changed time for meta data objects is now updated properly on changes.

* Deleting a table from the data dictionary now automatically removes any related joins.

* Fixed a bug where the field order wasn't being set properly for new fields.

* Fixed a bug with automatic plugin compilation using the wrong .NET assemblies.

* Fixed several issues that occurred when importing legacy projects. 

* Fixed a bug with imported projects not having the correct project ID.

* Fixed an issue where an expired license caused the application to stop working.