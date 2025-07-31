---
layout: default
title: What's New in this Release
nav_order: 2
parent: Home
---

# Version 1.4

* The primary navigation control in [Studio]({% link _docs/studio/working-with-studio.md %}) for interacting with the data dictionary has been replaced. The previous control had issues with performance and scrolling that were difficult to fix due to how it worked. The new control has much better performance, and always maintains the correct scroll position even after updating to accomodate new items. The new control also supports navigating with the arrow keys and spacebar on a keyboard, similar to the desktop version of Studio. 

* The context menu for [previewing tables]({% link _docs/studio/datadictionary/view-table-contents.md %}) in the previous control has been replaced with a preview button. 

* When previewing table contents in Studio, columns with errors are detected automatically and removed from the query so the remaining fields can still be inspected. This means that a single calculated field with a syntax error in the expression will no longer prevent the entire table from being previewed. 

* A new configuration setting, [Login Failure Limit]({% link _docs/studio/configuration/configuration-settings.md %}), allows you to define the number of failed login attempts are allowed before being restricted for 5 minutes. The default limit is 5 login attempts, and can be disabled by setting to 0. 

* [External authentication]({% link _docs/how-to/externalidentproviders.md %}) now supports a reporting_roles claim. If present, any users created as part of a single sign on attempt will have those roles attached.

* [External authentication]({% link _docs/how-to/externalidentproviders.md %}) in a tenant based project can now pass a claim named reporting_tenant in case a claim named tenant is already in use.

* A new toggle is available in [Studio]({% link _docs/studio/working-with-studio.md %}) that will globally disable the scheduler. This is handy if you want to test a copy of a live/production reporting project in a lab environment, but don't want the schedules to be sent with sample data. 

* It's no longer possible to [create a project]({% link _docs/studio/creating-a-project.md %}) with a blank name.

* You can now define multiple data sources even if [Allow Multiple Data Sources]({% link _docs/studio/configuration/configuration-settings.md %}) is disabled for a project. This allows you to use the built in connection string or DSN manager to define data sources for a tenant based project. 

* In Studio, you can now search the [data dictionary]({% link _docs/studio/datadictionary/index.md %}) by version as well as name.

* Sorting data dictionary items now ignores case and special characters for a more logical ordering. 

* If a report belongs to a [tenant]({% link _docs/studio/multi-tenant.md %}), it will now always retrieve data from that tenant's data source. This means that you can run and edit tenant based reports and test them against a tenant's data source while logged in with an Administrator account. 

* The [configuration section]({% link _docs/studio/configuration/configuration-settings.md %}) in Studio has a new Email tab where you can define Default email settings to use for the scheduler when a user hasn't defined custom settings. If you previously used the "Use as default settings for all users" option for this purpose, those settings will get automatically imported to the new location.

* The report files are once again persisted to a subfolder called "Reports" in the App_Data folder. In the previous 1.3 release, report storage moved from disk based individual files to a database table for improved performance. Reports aren't automatically imported to the report database from this folder, but they are much easier to back up when stored as individual text files on disk. 

* The [default table]({% link _docs/studio/configuration/configuration-settings.md %}) for a new project is now automatically set to the first table discovered during the scan. 

* The forms for editing [databases]({% link _docs/studio/datadictionary/database-properties.md %}), [tables]({% link _docs/studio/datadictionary/table-properties.md %}), [fields]({% link _docs/studio/datadictionary/field-properties.md %}), and [joins]({% link _docs/studio/datadictionary/relation-properties.md %}) now have change detection which disables the Save button until changes are made. 

## Bug Fixes

* Fixed an issue with the Display related field setting not working.

* Fixed an issue with access rights not being applied properly to a report when importing an entire project.

* Fixed an issue with calculated fields sometimes referencing themselves in the fields involved list.

* Fixed an issue with custom images like logos not being loaded.

* The total repeats possible for a recurring scheduled task can no longer exceed the day. This fixes an issue where a repeating task could interfere with a previous version of itself.

* Fixed an issue with Studio link sometimes not appearing for administrators.

* Fixed a bug that would occasionally cause a new table to be created during a data dictionary refresh, rather than updating the proper existing entry.

* Fixed a schema discovery issue with MySQL databases.

* Fixed an issue with transient lookup fields appearing to end users in the report wizards.

* Fixed an issue with user roles not being re-loaded properly after a restart.

* Fixed a redirect loop that would sometimes occur when setting up a fresh project. 

* Fixed a bug with the connection string manager not handling new data sources when added to an existing project.

* Updated several dependecies to fix reported vulnerabilties. 

* Fixed a very rare issue where an outer join in a query would cause the primary key constraint from the parent in the join to be retrieved along with the data.

* Fixed a bug where the weight of a new join would be 0, causing a pathfinding problem.

* Fixed a bug that prevented changing projects. 