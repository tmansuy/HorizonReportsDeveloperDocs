---
layout: default
title: What's New in this Release
nav_order: 2
parent: Home
---

# Version 1.3

* Horizon Reports has a new application database format that unifies storage for all application data (e.g. reports, templates, schedules, formulas, data sources, security objects).

* Horizon Reports now uses .NET 8

* Updating the connection string for a [database]({% link _docs/studio/datadictionary/database-properties.md %}) in Studio no longer requires a restart to take effect. 

* Swapped MySql.Data.MySqlClient provider with MySqlConnector since it works better with MariaDB

* Defined foreign keys in the database schema for a MySql database will now appear as corresponding [relations]({% link _docs/studio/datadictionary/relation-properties.md %}) for the table in Studio.

* You can now use [external authentication]({% link _docs/how-to/externalidentproviders.md %}) (Open ID Connect) with a tenant based project. 

* Externally authenticated users can now use 2-factor authentication.

* Data sources in the [connection string manager]({% link _docs/studio/datadictionary/database-properties.md %}) are now tested and saved one at a time, rather than all at once. 

* You can now save a connection string, even if a test connection fails. 

* The [connection string builder]({% link _docs/studio/datadictionary/connection-string-builder.md %}) is now available from a few new places.

* The report writer navigation button in Studio no longer requires a restart.

* If a project has more than one database, the source database name is displayed in the table caption when [creating a relation]({% link _docs/studio/datadictionary/relation-properties.md %}).

* If you change any [authentication settings]({% link _docs/studio/configuration/configuration-settings.md %}) for a project, you now get a warning that a restart is required for the changes to take effect.

* If the [authentication settings]({% link _docs/studio/configuration/configuration-settings.md %})for a project are causing a startup failure or a login problem, you can use the new command line parameter clearauthsettings=true. This allows you to start up the project locally while ignoring the authenticaiton settings to resolve the issue.

* Sql Server and MySql [project]({% link _docs/studio/creating-a-project.md %}) connection types also have a default connection string similar to SQLite.

* The Source Database field should now only appear if tenant support is off. You can also disable the field manually with a [new setting]({% link _docs/studio/configuration/configuration-settings.md %}).

* The installation folder now takes up less space and contains fewer files.

## Bug Fixes

* Fixed an issue where scrolling to the selected item in the database treeview sometimes scrolled to a previously clicked item.

* Fixed a bug where the database schema would be ignored during a refresh. 

* Fixed an issue where a project could get partially created and prevent the application from starting up.

* Fixed typos in a number of UI captions.

* Fixed a bug that allowed saving a join with an invalid field value.

* You can no longer create a project with a blank name.

* Fixed an issue with dynamic formatters not appearing properly in the list of available formats in Studio.
