---
layout: default
title: Migrating Stonefield Query Plugins
nav_order: 16
parent: Plugins
---

If you're migrating from a Stonefield Query Enterprise project to a Horizon Reports project, you'll need to update your plugins. To do so, make the following changes:

* Update the target framework to .NET 6

* Remove old references, and add the *HorizonReports.Api* nuget package

* Update the app object interface from ISQApplication to IHorizonReportsAppService.

* The interfaces IField, ITable, and IDatabase should be replaced with references to Field, Table, and Database

* The Application.Configuration object is split in to references to either Application.ProjectSettings or Application.AppSettings.


Making the above changes should be sufficient to migrate most plugins to the latest release. Create a <a href="https://www.horizon-reports.com/helpdesk/" target="top">support ticket</a> if you need further assistance with migrating your plugins.