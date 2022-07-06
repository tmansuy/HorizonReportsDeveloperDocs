---
layout: default
title: Creating a Virtual Table
nav_order: 5
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

A virtual table is one you define in the data dictionary and doesn't physically exist. When the user uses a virtual table in a report, [plugin code]({% link _docs/plugins/virtualtable/select.md %}) you create is used to retrieve the appropriate data.

Virtual tables are typically used to hide the complexity of an application's data structures. For example, if you have individual invoices and credit notes tables, you may wish to create a virtual table that combines records from both tables. That would make reporting much easier for the user.

You can create a new virtual table from scratch, or you can clone an existing table as a virtual table and then make the desired changes. To create a virtual table from scratch, click the Add button (![](/assets/images/addbutton.png)) beside the Tables node in the TreeView. Alternately, you can copy the fields and relations from an existing table by using the *Clone as Virtual Table* button from the table properties section of an existing table.

A virtual table needs a plugin that specifies how to retrieve data for the virtual table. There are several built-in plugins, such as ones that retrieve data using a SQL statement or from Microsoft Excel speadsheet; see the [Table Properties]({% link _docs/studio/datadictionary/table-properties.md %}) help topic for information on these plugins. You can also create your own [custom plugin]({% link _docs/plugins/virtualtable/index.md %}).

A virtual table can also be created automatically from a stored procedure in the database if you turn on the *Create virtual tables from stored procedures* option when you create a project or add a database to a project. See the [Table Properties]({% link _docs/studio/datadictionary/table-properties.md %}) help topic for information on such virtual tables.
