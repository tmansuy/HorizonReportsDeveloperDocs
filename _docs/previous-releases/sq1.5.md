---
layout: default
title: Stonefield Query 1.5
nav_order: 11
parent: Previous Releases
grand_parent: Home
---

# New Features

* Multi-tenant environments are now supported without having to write any custom plugins.

* Stored procedures are now supported without having to write any custom plugins. When a database is added to the data dictionary, you can optionally tell Studio to create virtual tables for any stored procedures. You can also view the contents of and refresh virtual tables created from stored procedures.

* Studio now has a function to find possible relationships between tables. This can save a lot of time in manually building relationships.

* Several new plugin methods are now available: BeforeLogin and AfterLogin in application plugins and BeforeReportCopied, AfterReportCopied, BeforeReportDeleted, AfterReportDeleted, AfterReportSaved, ReportCreated, and BeforeSQLStatementSentToDatabase in report engine plugins. Also, the GetParameters and Select methods of virtual table plugins and the Convert method of value converter plugins accept different parameters than before. Note that these are breaking changes; you'll need to apply these changes to any plugins you've already created and recompile them.

* You can now cause an error message to be displayed to the user from a plugin method by calling Application.MessageManager.RaiseErrorMessage.

* All calls to plugin methods are now wrapped in try structures and logged for better diagnostics.

* If your application makes changes to the data dictionary or security settings after Stonefield Query has been started, you can send a message to Stonefield Query telling it to refresh these settings without restarting. The new MessagingPort configuration setting specifies the port used for messaging.

* Stonefield Query now has fine control over which features user can access. For example, you can specify that members of a particular role can edit the properties of the fields in a report but not add or remove fields. To support this, a new User Resources panel was added to Studio and the "Non-admin users can edit tags" and "Non-admin users can schedule reports" configuration settings were removed.

* The new Icon File configuration setting allows you to specify the file used as the icon in the browser.

* If the new Allow Access to Reports When No Access to Fields configuration setting is turned on, users who don't have access to certain fields can see and run the reports containing those fields but the reports act as if those fields don't exist in the report.

* Set the new Send Support Tickets to Support Email Address configuration setting to True to indicate that support ticket submissions should be sent to a support email address instead of the usual support ticket system.

* The new Encrypt Connection Strings configuration setting specifies whether connection strings for the data dictionary, security, formulas, and tags databases are encrypted.

* You can now specify a dynamic expression for the format of a field. Also, more built-in field formats, especially for DateTime and TimeSpan fields, are now available and formats now appear as "{0: format }".

* The Publish Project dialog no longer remembers the user name and password for FTP sites for security reasons. However, it does remember folder names.

* Stonefield Query can now work in a subfolder of an existing application, such as http://www.myapp.com/reporting.

* You can now specify that delimiters are added to all names when creating a project or adding a database to an existing project.

* You can now call Stonefield Query from another web application and pass a security token rather than the user name and password as part of the URL. In addition, you can specify the name of a report to automatically run.

* The Allow Values setting is now disabled for Boolean fields since there are only two obvious choices.

* Stonefield Query and Studio now both support connections to Microsoft SQL Server using System.Data.SqlClient rather than ODBC or OLE DB.

* The error dialog now has a help button that display help about what to do when an error occurs.

* Report permissions are now stored in the Permissions security table rather than in the SFX file. Also, the Permissions table now contains ResourceName and RoleName columns for readability.

* All third-party libraries, such as Ninject, Entity Framework, and Bootstrap, were updated to the latest releases. Stonefield Query now uses MVC 5 and version 4.5 of the .NET framework.

* Improvements were made in the Convert Reports function.

* The Pervasive database engine is now better supported.

* Formulas on fields added dynamically to the data dictionary are now supported.

## Bug Fixes

* Opening an existing desktop project and then cancelling the conversion dialog no longer closes any open project.

* Converting an existing desktop project twice in one sitting no longer causes an error.

* A bug that caused an error publishing to a folder was fixed. Also, the App_data and Licenses folder are now created and all necessary .config files and the image files specified in the Logo Image File and Icon File configuration settings are now published, and the folder you specify in the Publish dialog is now created if it doesn't exist.

* A bug that caused an error tabbing out of the Plugin Data control in the Calc page of the field properties pane was fixed.

* A bug that caused an error viewing table contents in Studio was fixed.

* Editing a report outside of Stonefield Query no longer causes fields to be duplicated when it's reloaded.

* A bug that caused a report engine AfterSQLStatementCreated method to always receive null for the report was fixed.

* An issue with storing the Tags, Users, Roles, UserRoles, and Permissions tables in another database engine such as SQL Server rather than the default SQLite was corrected.

* The Advanced Report Designer can now edit a report even if no records are returned from the query. However, note that fields may not be sized optimally.

* The DateDiff function now ignores the time component so it gives consistent results when used in conjuction with the Now function.

* A bug that caused an error when a report contains a field with the same name as its table (such as Tax.Tax) was fixed.

* Stonefield Query now properly handles the case where a data engine plugin's GetDataSources method throws an exception.

* An issue that caused certain routes returning not found (400) HTTP errors for post requests was fixed.

* Filtering on a field with a value converter now works properly.

* A bug that caused Sortable and Content Type to be set improperly for non-sortable and image fields while reading the structure of a database was fixed.

* You can no longer create a virtual table or subtable of a virtual table.

* A bug that caused an error under some conditions when selecting a virtual table created from a stored procedure was fixed.

* A bug that caused an error when updating the security tables to the latest structure when those tables are stored in Microsoft SQL Server was fixed.

* Security.Setup now throws an exception if a Tables table exists in the security database, meaning the developer has both the security and data dictionary tables in the same database.

* A bug that caused an error when two fields had the same name but different case was fixed.

* An error that sometimes occurred when starting Stonefield Query due to missing information in the data sources roles file was fixed.

* Create a report as one user, logging out, logging in as another user, and then editing the report now saves the correct user name for the report's ModifedBy property.

* You can now use the DATEPART function in an expression of a formula or calculated field.

* A issue running reports against SQL Server under some conditions was fixed.

* If a custom plugin fails to load (such as if the interface wasn't updated with breaking changes), stock plugins continue to load correctly.