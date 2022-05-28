---
layout: default
title: Stonefield Query 2.0
nav_order: 8
parent: Previous Releases
grand_parent: Home
---

# New Features

* Any place where you enter a connection string now has a Build button to display a dialog allowing you to visually create the connection string.

* Studio can generate C# plugin source code for you. To create a value converter or values method plugin for a field, click the new buttons in the Calc page for the field. To create a plugin for a virtual table, click the new button in the properties pane for the table. To create other types of plugins, choose the Create Plugin function in the File menu.

* The Find Field and Find Next Field functions in the Edit menu and the toolbar allow you to find a field having some text in the Name or Caption properties.

* You can now reload security and the data dictionary without restarting the web server or application pool.

* There are two new configuration settings: Conn. String for Stonefield Query Data and Provider for Stonefield Query Data. These are used as the connection settings for the security, formulas, and tags databases instead of hard-coded as SQLite using SQData.dat.

* You can now edit the Name property of a field in a virtual table.

* You can now edit the Name property of a real field or table by double-clicking the "Name" label to the left of it. This should only be used rarely, since the correct way to update a real table is using the Refresh function.

* A new Calculated checkbox in the Calc page for fields allows you to indicate whether a field in a virtual table is real or calculated. This checkbox is disabled for fields in real tables.

* The Fields Involved control in the Calc page for fields is now always available, even for real fields, in case a value converter needs other fields in the query. Internally, this meant moving the FieldList property from ICalculatedField to its parent IField.

* The Format drop-down list for fields now includes 12 and 24-hour formats for TimeSpan fields.

* You can now select a calculated field as a parent or child field in a join.

* There's a new IReportBase interface that's the parent of IReport; this provides a base interface for all reports, including dashboards.

* The AfterSQLStatementGenerated method of report engine plugins is passed a new DataSourceName parameter containing the name of the current data source being accessed in case a plugin needs to use specific code for different data sources. Also, many of the methods now accept IReportBase rather than IReport parameters. Note that these are breaking changes, so you'll need to update any report engine plugin you've created and recompile the plugin.

* You can now run Stonefield Query in an IFrame. This can be turned on and off using the "supportiframes" setting in web.config.

* You can now specify the values of ask-at-runtime filter conditions when running a report from another web application. The user is not prompted for any values passed this way. Also, when running a report from another web application, the report now displays in the preview window without the rest of the UI appearing.

* There's now better support for the Pervasive database engine.

* IConditionValue and IFilterCondition now have ErrorMessage properties so you can determine what error occurred when evaluating expressions in condition values.

* Connection classes now have ConnectionTimeout and CommandTimeout properties, allowing you to configure them as necessary in a plugin. They also have a DataSource property containing the name of the current data source being accessed in case a plugin needs to use specific code for different data sources.

* The data engine does a better job of handling thread-unsafe plugin code.

## Bug Fixes

* Many new reserved words were added to the list of keywords Studio automatically delimited when used as a table or field name.

* Testing relations using delimited table or field names now works properly.

* Turning off Enumerated Values or Display Field From Related Table is now properly saved.

* A better error message is now displayed if something goes wrong when publishing a project.

* The Format and Default Summary drop-down lists now display the correct set of choices when a field has a value converter and the data type is different than that of the field.

* If the Order property of a database is changed, other databases are reordered as necessary.

* Some issues with converting reports were fixed.

* The field name shown in the TreeView no longer displays delimiters when the name is edited.

* Studio now handles it if you select the Project_Data folder rather than its parent folder when opening a project.

* You now get a warning if more than one relationship exists between a pair of tables.

* An issue with displaying the contents of tables in Studio was fixed.

* Non-thread-safe ReportEngine plugins are now handled better (although we recommend using thread-safe code for plugins).

* Renaming a table in Studio now works properly.

* Virtual table plugins that don't properly handle aliased columns are now handled properly.

* Expressions can now use any operator type for comparisons.

* The SQL statement builder now respects the Stonefield Query Performs Joins configuration setting.

* There is no longer a conflict between diagnostic logging in Studio and in SQWeb.