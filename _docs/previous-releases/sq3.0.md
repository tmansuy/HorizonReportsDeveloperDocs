---
layout: default
title: Stonefield Query 3.0
<<<<<<< Updated upstream
nav_order: 8
=======
<<<<<<< Updated upstream
nav_order: 7
=======
nav_order: 9
>>>>>>> Stashed changes
>>>>>>> Stashed changes
parent: Previous Releases
grand_parent: Home
---

# New Features

* Fields have a couple of new properties: Appears In and Output Type. You can set Appears In to as many tables as you wish to make this field appear as if it belongs to those tables; that is, this field shows up in the field list when you select one of those tables in step 2 of the report wizards. This is similar to the Display Field From Related Table feature but doesn't require creating a calculated field in each table. Output Type, which specifies the data type for the field as it appears in the result set for a report, is normally set automatically for a field using a value converter but there may be times when you have to set it manually.

* You can now choose a value converter for a calculated field.

* New value converters are available: LookupFieldConverter, StringToDateTimeValueConverter, ExcelDateToDateTimeValueConverter, and NumericToBoolValueConverter.

* The new User Can Manage Connection String value for a database's Connection Type property allows you to define the connection string for the database at runtime (in the Setup Wizard) without having to create a DataEngine plugin to set the connection string.

* There's a new How to Filter on Unfavored Table option for relations that defines how a filter condition on the unfavored table of an outer join is treated. There's also a related DefaultHowToFilterUnfavoredTable configuration setting.

* You can now use "." as an operator in formulas and calculated fields. For example, an expression like (Orders.ShippedDate * Orders.OrderDate).TotalHours, which determines the number of hours between when an item was ordered and when it was shipped, is now supported.

* The Enumerated Values feature now works with Boolean fields.

* Selecting a join for a join tree now adds all the joins each of the tables in that join have to the Relations list.

* When you add a field to a virtual table in the data dictionary, you can indicate whether it's a calculated field or not by setting the Calculated property accordingly.

* If you add a MySQL database to the data dictionary and specify something other than `` (the normal MySQL name delimiters) as the delimiters, you are asked whether you wish to use `` instead.

* The Update Virtual/Subtable to Match Main Table function now asks whether you want to update the Caption, Heading, and Comments properties.

* The MySQL ADO.NET provider from Oracle is now supported.

* Subqueries are now supported in complex join expressions.

* Stonefield Query now supports more than one table with the same name but different schemas or owners.

* Studio now supports updating the version number of tables and fields that no longer exist in database because they were removed in a newer version when you refresh the data dictionary. You are also prompted whether a table or field should be removed from the data dictionary if it isn't versioned.

* Relationships can now be read from more database engines.

* You are now prompted for a name when creating a subtable or virtual table.

* The setting of the Add Delimiters to All Names option when adding or refreshing a database is now saved, and that setting cannot be turned off once it's turned on.

* You can now edit the Type property of a real field by double-clicking the "Type" label to the left of it. This should only be used rarely, since the correct way to update a real field is using the Refresh function.

* Breaking change: IStonefieldQueryValueConverterPlugin now has Report and AliasList members. You must edit any custom value converter you created to add these properties and rebuild the DLL.

* Some value converters and virtual table plugins now have builders to assist with editing the data for the plugin. If a builder is available, click the button with the ellipsis ("...") beside the Value Converter Data or Plugin Data setting.

* Two new types of virtual tables are available. The SQLStatementPlugin virtual table plugin uses the SQL statement and parameters specified in the plugin data to generate the virtual table; this is handy if you don't want to or can't create a view in the database. The ExcelToTablePlugin virtual table plugin reads from a Microsoft Excel document so you can query on Excel documents as easily as a database. Builders make it easy to set these up and even create the fields in the data dictionary for the tables.

* New value converters are available: LookupFieldConverter, StringToDateTimeValueConverter, ExcelDateToDateTimeValueConverter, and NumericToBoolValueConverter.

* You can now edit the C# plugin source code Studio generated for you with a single click in Studio rather than having to find the solution and open it manually in Visual Studio.

* You can now create a Functions plugin from the Create Plugin function.

* A virtual table plugin can populate the new AvailableValues collection of the Parameter class with options for user selection, and the UI will present those as optional values for the parameter.

* If a functions plugin class has a member of type ISQApplication, that member is automatically set to a reference to the application object, since many functions need access to the database, data dictionary, or other things available through that object.

* Formatter plugins can now support multiple types. This isn't a breaking change: because the constructor for the StonefieldQueryFormatter attribute uses "params Type[] types", a single type can still be passed as well as a comma-delimited list or array of types.

* The new Create SQLite Data Dictionary function in Studio creates a SQLite version of your data dictionary if it uses a different database engine. This is handy for support purposes, as you can easily send the resulting DAT file to Stonefield for analysis.

* The new Display Help function allows you to view the generated help anytime you wish.

* Studio has a new Export to Microsoft Excel function.

* The Publish process now shuts down the application pool on the web server before copying files so you don't have to do it manually (or get an error message that files couldn't be copied if you didn't).

* The Publish dialog now has an option to only publish project data. This is a much smaller upload when the only changes are to project data, not to program files.

* Stonefield Query Studio uses a new icon so you can distinguish it from our desktop version if you have both installed.

* The View Table Contents and View Field Contents functions now retrieve a maximum of 1,000 records rather than the entire table.

* The new Set Contact Information in the Help menu allows you to edit the contact information used for error reporting.

* The new Register Scheduled Task as Same User Task Runs Under configuration setting allows you to address a security issue when creating tasks from the IIS "DefaultAppPool" identity.

* The Trim function now removes trailing null values as well as spaces.

* The Char and Chr functions now return a string rather than a char value char is rarely used and this saves having to use Char(x).ToString() in a formula.

* The new InList function determines if a set of values contains the specified value.

* A new variant of the LTrim function removes any character from the start of a string.

* Additional members have been added to many classes; see the Stonefield Query Object Model for complete documentation for all classes.

* You can now create your own custom log files using a CustomLogger.config file. If that file is present in the Logs folder, it's used instead of Logger.config file for settings. The benefit of using such a file rather than modifying Logger.config is that it won't be overwritten when a new version of Stonefield Query is released.

* Stonefield Query now supports locale-specific resource files such as resources.FR-fr.xml If present, they take top priority over language resources.

* Custom settings defined in your project can now be displayed in reports.

* To deploy sample or standard reports, create a folder named StockReports in the Project_Data folder and copy the SFX files for the reports to that folder. When Stonefield Query starts, it looks for any new or modified reports in that folder and copies any it finds to the App_Data\Reports folder.

* A similar mechanism is used for templates: if you wish to deploy your own set of templates rather than the ones Stonefield Query comes with, create a folder named StockTemplates in the Project_Data folder and copy the SQT files for the templates to that folder. When Stonefield Query starts, it looks for any new or modified templates in that folder and copies any it finds to the App_Data\Templates folder.

* If the new ImpersonateSchedulerUser setting in Settings.xml is set to true, the scheduler registers the task as the same user the task runs under. This addresses a security issue when creating tasks from the IIS "DefaultAppPool" identity.

* When converting from an existing desktop project, you can fine-tune the conversion process using custom code in SQConvert.sqs. Also, you can use a project-specific version of CalcFieldsConversion.xml.

## Bug Fixes

* Expressions using database functions prefixed with a schema are now supported.

* The ResultSet property of the report passed to the AfterDataRetrieved method of a plugin is now the correct value instead of null.

* Changes made to a report with AutoFitToPage set to true in an AfterCreateLayout plugin method are now respected.

* A bug that didn't set the default value for new columns added to data dictionary tables stored in SQL Server was fixed.

* If the Heading property of a field changes in the data dictionary but the user didn't change the heading in a report, the updated heading is now used in the report.

* Byte fields are now supported in filter conditions.

* Subqueries, such as when an exclude filter condition is used, now work properly when a subtable is used.

* Previously, if you created a calculated field but didn't fill in the Expression, it was treated as a real field. This has been fixed.

* Stonefield Query now properly handles the case where the Fields Involved property of a field includes the field itself.

* Some missing assemblies needed by the Advanced Report Designer were added to the Bin folder.

* Studio now handles the case where two databases have the same name: it now asks for a new logical name for the second one.

* The Test function in the connection string builder dialog now handles error more gracefully.

* The Find Field function is no longer available for any panel other than Databases.

* Editing the Caption for a table or reverting changes to a table or field no longer adds delimiters to the name in the TreeView.

* A bug that caused an error in Studio when using the Update Virtual/Subtable to Match Main Table function was fixed. A related bug that caused Fields Involved and Expression to not be updated properly under some conditions was also fixed.

* A bug that caused an error when turning off the Reportable property for a field when Studio is configured to not display non-reportable objects was fixed.

* A bug that removed tables and fields from a database that wasn't being refreshed when another was was fixed.

* A bug that gave a warning about not being able to publish the Plugins or Functions folder when publishing a project was fixed.

* The Publish function now removes any older assemblies that may cause problems with a newer version of Stonefield Query.

* Certain reserved words are no longer automatically delimited. For example, although it's a reserved word in most database systems, USER isn't a reserved word in MySQL and adding delimiters to it prevents Stonefield Query from being able to retrieve that field from the database.

* The values for enumerated fields can now handle "&" and other illegal XML characters.

* The Convert Reports function now supports chart reports correctly. Bugs in handling missing templates and linked reports were also fixed.

* The connection string builder now adds "trusted_connection=yes" to the connection string if the user name and password aren't specified.

* The Test Relation function now works better with tables in different databases and using complex joins using functions such as CAST or CONVERT.

* A bug in refreshing a single table using ADO was fixed.

* A bug in handling expressions for calculated fields when there's more than one table with the same name but in different databases was fixed.

* The installer no longer gives a warning if a version of IIS Express newer than 8.0 is already installed.

* An issue with projects using shared connections was fixed: If a report has only tables from a single database and it isn't the non-shared database, database prefixes are added as necessary.

* A bug where changing the current culture in the Options dialog wasn't changing that culture for the user until the server was restarted was fixed.

* If a virtual table's plugin is missing, Stonefield Query is no longer prevented from starting up; instead, the user gets a warning when that table is used in a report.

* A bug that caused the wrong fields to be displayed for a relationship when changing one of the tables to one that has fewer fields than the previous one was fixed.

* Queries against MySQL and SQLite databases now use LIMIT rather than TOP clauses since the latter isn't supported in those engines.

* Queries against MySQL databases now use the correct syntax for the "contains" operator in filter conditions.

* Custom value converter plugin code generated by Studio is now flagged as custom rather than stock.

* Virtual table plugin code generated by Studio no longer has extra spaces in several places.

* A bug that prevents user resources from being removed was fixed.

* If you refresh a database that was added with the Add Delimiters to All Names option turned on but have that option turned off in the Refresh dialog, the refresh process no longer adds duplicate table and field names.

* You can no longer edit the name of an object in the TreeView; you have to do it using the Name textbox.

* Several issues converting projects from the older desktop version of Stonefield Query were resolved.

* The message manager now directly calls the message handler for a message rather than having the method fire in a new thread. The former method is causing
problems when called from an ASP.NET controller action that doesn't support async.

* Creating a relation on a field no longer changes the selected field if the child and parent table have other fields that match names.

* The Field Order dialog now displays the field name and caption properly when the Display Captions After Object Names setting is turned on.

* Non-reportable calculated fields now display with an appropriate icon in the TreeView.