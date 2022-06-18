---
layout: default
title: Table Properties
nav_order: 3
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

There are three types of tables:

* Real tables - these physically exist in the database.

* Virtual tables - tables that you define and don't physically exist. When the user uses a virtual table in a report, plugin code is used to retrieve the appropriate data. 

* Subtables - these are used to resolve self-joins or multiple relationships between tables.

When you select a table in Studio, an editor displays the properties for that table:

![](/assets/images/tableprops.png)

* *Name*: the name of the table. If the name contains characters other than letters, numbers, and underscores, or if it matches a SQL keyword, such as DESC or ORDER, Studio automatically adds delimiters around the name (the delimiters defined in the [database properties]({% link _docs/studio/datadictionary/database-properties.md %})). It also automatically adds delimiters if you turned on the *Add delimiters to all names* setting when adding or refreshing the database. You can also manually add delimiters if necessary.

* *Caption*: the name as displayed to the user in the report writer. If the caption is an expression that should be evaluated, surround it with curly braces. For example, if the caption calls the GetCaption [plugin]({% link _docs/plugins/index.md %}), specify "{GetCaption()}" (without the quotes) for the caption. Note the expression is evaluated every time the table is accessed, so you get better performance by changing the caption in the [AfterLoaded]({% link _docs/plugins/datadictionary/afterloaded.md %}) method of a data dictionary plugin instead.

* *Data groups*: the data group or groups the table belongs to (see the [Creating a Data Group]({% link _docs/studio/creating-a-data-group.md %}) topic for information on data groups). To change the data group for the table, click the drop-down button to display a list of the defined data groups and turn on or off the checkmarks in front of the appropriate data group names. Click the drop-down button again to close the list.

* *Roles*: the roles that can access the table (see the [Creating a Role]({% link _docs/studio/creating-a-role.md %}) topic for information on roles). Leave this property blank to allow all users to access it. To change the roles that can access the table, click the drop-down button to display a TreeView of the defined roles and turn on or off the checkmarks in front of the appropriate role names. Click the drop-down button again to close the list.

* *Version*: the table's [version number]({% link _docs/studio/datadictionary/versioning.md %}). A blank value means the table is not versioned: it appears in the report writer regardless of the version of the database. For a table that isn't available in every version of the database, enter the version number followed by "+" to indicate the table appears in that version and higher versions and should not appear in lower versions (that is, the table was added in that version), "-" to indicate the table appears in that version and lower versions and should not appear in higher versions (that is, the table was removed in the next version), or no suffix to indicate the table appears only in that version and should not appear in any other version. For example, "5.3+" indicates the table is available starting in version 5.3 while "5.3-" indicates it was removed in version 5.4.

    Use a comma-delimited list of values if the table was added in one version and later removed. For example, "5.3+,5.5-" means it was added in version 5.3 and removed in version 5.6.
	
* *Virtual*: if this property is turned on (which it is by default for tables you create in the data dictionary), this table will call a plugin for data retrieval.

* *Reportable*: if this property is turned on (which it is by default), the user can query on fields from this table. Turning this off means the table won't appear anywhere in the report writer. This is handy for "system" tables or tables you don't want the user to ever query on.

* *Do not refresh*: turn this setting on if you don't want this table refreshed when you [refresh the data dictionary]({% link _docs/studio/datadictionary/refreshing.md %}).

* *Plugin*: this property, which is only available for virtual tables, indicates the name of the plugin used to retrieve data for the virtual table. The choices available are:

    * *CombinedVirtualTablePlugin*: this built-in plugin combines the records of two tables with identical structures into one. For example, the AccountMate accounting system has a table named ARTRAN that contains current period accounts receivable transactions and a table with the same structure named ARYTRN that contains historical transactions. Because users often want to report on all transactions, a project that reports on AccountMate has a virtual table named ARTRN that uses CombinedVirtualTablePlugin to execute SQL statements against ARTRAN and ARYTRN and combine the results into a single result set. To tell the plugin which tables are used, *Plugin data* contains the names of the two tables, each on its own line.

    * *ExcelToTablePlugin*: this built-in plugin reads from a Microsoft Excel document so you can query on Excel documents as easily as a database.

    * *SQLStatementPlugin*: this built-in plugin uses the SQL statement and parameters specified in *Plugin data* to generate the virtual table; this is handy if you don't want to or can't create a view in the database.

    * *StoredProcedurePlugin*: this built-in plugin calls the stored procedure whose name is in *Plugin data* to retrieve the data for the virtual table. The user is prompted for the values of any parameters required by the stored procedure. When you save a table using this plugin, you are prompted to refresh the table so the list of fields is correct.

    * Your plugin names: the list includes the names of any [virtual table plugins]({% link _docs/plugins/virtualtable/index.md %}) contained in DLLs in the Project_Data\Plugins folder.

* *Plugin data*: this property, which is only available for virtual tables, contains data needed by the plugin specified in *Plugin*. For example, for CombinedVirtualTablePlugin, *Plugin data* contains the names of the two tables, each on its own line. For StoredProcedurePlugin, it contains the name of the stored procedure. Your own virtual table plugin can use the value of *Plugin data* for its own purposes.

* *Custom properties*: Horizon Reports doesn't use this property for anything. You can use it to hold any information you wish. The value is stored in the UserDefined property of the Table object, which a [plugin]({% link _docs/plugins/index.md %}) could use for any purpose necessary.

