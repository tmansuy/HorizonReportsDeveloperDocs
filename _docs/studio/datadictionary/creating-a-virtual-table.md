---
layout: default
title: Creating a Virtual Table
nav_order: 5
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

A virtual table is one you define in the data dictionary and doesn't physically exist. When the user uses a virtual table in a report, [plugin code]({% link _docs/plugins/virtualtable/select.md %}) you create is used to retrieve the appropriate data.

Virtual tables are typically used to hide the complexity of an application's data structures. For example, if you have individual invoices and credit notes tables, you may wish to create a virtual table that combines records from both tables. That would make reporting much easier for the user.

To create a virtual table, click the Add button (![](images\addbutton.png)) beside the Tables node in the TreeView. A dialog will appear where you can specify the type of new table (choose virtual table). Enter the desired name for the new table. You can optionally copy the fields from an existing table. Studio creates a copy of the table and all of its fields and relations.

A virtual table needs a plugin that specifies how to retrieve data for the virtual table. There are several built-in plugins, such as ones that retrieve data using a SQL statement or from Microsoft Excel speadsheet; see the [Table Properties]({% link _docs/studio/datadictionary/table-properties.md %}) help topic for information on these plugins. You can also create your own [custom plugin]({% link _docs/plugins/virtualtable/index.md %}).

A virtual table can also be created automatically from a stored procedure in the database if you turn on the *Create virtual tables from stored procedures* option when you create a project or add a database to a project. See the [Table Properties]({% link _docs/studio/datadictionary/table-properties.md %}) help topic for information on such virtual tables.
