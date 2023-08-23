---
layout: default
title: Horizon Reports 1.0
nav_order: 2
parent: Previous Releases
grand_parent: Home
---

# Version 1.0

* Stonefield Query Enterprise is now called Horizon Reports. The functionality that was previously located in the separate Stonefield Query Studio tool is now part of the [web application]({% link _docs/studio/index.md %}). As a result, Horizon Reports only has one installer that can be used for both development and production environments.

* Horizon Reports now uses .NET 6. This means that [plugins]({% link _docs/plugins/index.md %}) will need to be recompiled in order to work with this release. Make sure to update the references in your plugin code from Stonefield/Stonefield.Query to HorizonReports.

* The Horizon Reports API is now available as a [Nuget package](https://www.nuget.org/packages/HorizonReports.Api). When [updating plugins]({% link _docs/plugins/migrating.md %}), remove old references to Stonefield Query assemblies and add a reference to HorizonReports.Api on nuget instead.

* Horizon Reports now uses entity framework to store the project and data dictionary settings, and supports SQLite, SQL Server, or MySQL/MariaDB. The first time you launch the new version, you'll be prompted to enter the connection information for a new database. Afterwards, you can edit the [hrsettings.json]({% link _docs/how-to/configuring.md %}) file to make changes to the connection settings. If there's already a previous Stonefield Query Enterprise project in place, it will be [imported]({% link _docs/studio/importing-a-project.md %}) automatically.

* Horizon Reports now uses the NLog logging package instead of log4net to generate [application logs]({% link _docs/how-to/diagnostics.md %}). If you previously used a custom logging provider file with log4net, please contact support for assistance. 

* Creating a log support package now includes archived logs as well.

* When using the MariaDB [ODBC driver]({% link _docs/studio/datadictionary/adding-a-database.md %}), MySQL specific connection settings are now used.

* You can now bypass [external authentication]({% link _docs/how-to/externalidentproviders.md %}) by passing a username and password as URL parameters. You could use this to log in with an Administrator account if necessary. 

## Bug Fixes

* Fixed an issue that caused usage tracking to not work if you used a provider other than SQLite for your project.

* Problems with plugins or function assemblies should no longer prevent the application from starting.

* Studio now ignores stored procedures that don't have an assigned schema.

* Fixed handling of currency types during data dictionary discovery.

* If you have a custom output plugin, the file name passed to "PerformOutput" will now contain a timestamp if the user turned that option on.

* Fixed a bug with OpenIDConnect not using the correct response type. 