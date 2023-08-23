---
layout: default
title: What's New in this Release
nav_order: 2
parent: Home
---

# Version 1.2

* Horizon Reports will now run in a Linux environment. A [docker image]({% link _docs/deploying/docker.md %}) is available for this purpose.

* A new [project setting]({% link _docs/studio/configuration/configuration-settings.md %}), Disable Slide Toggles, allows you to disable the "slide" style toggle switches and show standard checkboxes instead.

* You can now show captions beside object names in the [database treeview]({% link _docs/studio/datadictionary/index.md %}) in Studio.

* A new option in Studio allows you to [hide non-reportable tables and fields from view]({% link _docs/studio/datadictionary/index.md %}).

* The same [connection string builder]({% link _docs/studio/datadictionary/connection-string-builder.md %}) in Studio is now available when creating a new project.

* A new Ignore Schema option when [refreshing]({% link _docs/studio/datadictionary/refreshing.md %}) allows you to ignore the schema value when matching objects. This is useful if you want to refresh against a database type that doesn't support schemas, but use an existing project with schema names to do so.

* Administrators can now log in even if there's a problem with the license file.

* You can now navigate directly to Setup from Studio.

* More relevant error information is displayed in the browser when a connection test fails.

* Loading/busy indicators are now shown when testing joins and connections.

* A new reload button is available in the license manager. You can use this to force the [licenses]({% link _docs/how-to/activating.md %}) to be reloaded if you made changes to the license file on disk.

* The data source name is now used as the database name when creating a project based on a SQLite database.

* You can now create new database fields (rather than Calculated fields) in Studio. In addition, you can now change the name and data type for existing [database fields]({% link _docs/studio/datadictionary/field-properties.md %}).

* Studio will now automatically reload if you [delete the project]({% link _docs/studio/managing-projects.md %}) that's currently open.

* Added confirmation prompt when deleting a project.

* You can now use Studio without having a [developer license]({% link _docs/licensing.md %}) installed.

* A Project_Data folder is now created automatically if it doesn't exist when running for the first time.

* Data protection keys are now persisted and reused when the application restarts.

## Bug Fixes

* Fixed a bug with custom user resources not being loaded from the project file.

* Fixed a bug with related/involved fields not being saved properly for calculated fields.

* Fixed a bug with built-in functions not getting loaded if a Functions folder didn't exist. 

* Fixed an issue with unlimited viewer licenses not being handled properly.

* Fixed a bug where the list of available tables shown during a refresh was sometimes empty.

* Fixed an issue where the table preview wasn't being updated to reflect the most recent changes.

* Fixed a bug with involved fields sometimes not being added to the SQL query if a complex join was used in the report.

* Added delay to search in Studio to improve performance in large projects.

* Fixed a bug when creating a subtable that had a field with the same name as the original table.

* Fixed a bug with SQL Passthrough reports not working initially after creation.

* Fixed a bug with getting logged out automatically after creating a new project.
