---
layout: default
title: Adding a Database
nav_order: 1
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

Filling in the data dictionary for a database would be a very tedious process if you had to do it by hand. Fortunately, Horizon Reports Studio has a feature to "discover" the metadata for a database. You do this by adding a database to the current project's data dictionary.

To start the process, click the Add button (![](/assets/images/addbutton.png)) beside the Databases node in the TreeView. The Add Database dialog appears.

![](/assets/images/adddatabase.png)

* *Name delimiters*: Specify which characters to use as delimiters around table and field names that need delimiters (for example, names with spaces in them). Specify a two-character value, with the first character being the left delimiter and the second being the right. Examples are "", meaning use double quotes, and [], meaning names are delimited with square brackets. MySQL needs the reverse apostrophe: ``

* *Add delimiters to all names*: Turn this setting on if you want delimiters added to all names. When off, Studio automatically adds delimiters to table and field names it thinks need them: names containing illegal characters such as spaces or names using keywords such as TABLE. 

* *Connection string*: Enter the connection string for the application database you'd like to query against. Horizon Reports will use this connection to "discover" the metadata for a database, including all of its tables, fields, and relationships.

    For ODBC, the connection string is typically something like "driver=*ODBC driver name*;server=*server name*;database=*database name*;uid=*user name*;pwd=*password*."

    For OLE DB, the connection string is typically something like "Provider=*OLE DB provider name*;Data Source=*server name*;Initial Catalog=*database name*;User ID=*user name*;Password=*password*."

    For SqlClient (the .NET provider for Microsoft SQL Server), the connection string is typically something like "Provider=System.Data.SqlClient;Server=*server name*;Database=*database*;User ID=*user name*;Password=*password*."

    See <a href="http://www.connectionstrings.com" target="top">www.connectionstrings.com</a> for connection strings for different ODBC drivers and OLE DB providers.


* *Include views*: Turn this setting on if you want views included in the discovery.

* *Create virtual tables from stored procedures*: With this option on, Studio creates virtual tables for any stored procedures in the database. 

* *Create subtables for self joined tables*: Turn this option on to automatically create a subtable any time any self-joined table or more than one relationship between the same set of tables is discovered. You can rename the subtable if you wish. See the [Creating a Subtable]({% link _docs/studio/datadictionary/table-properties.md %}) topic for information on subtables.

Once you've filled in all the information in this dialog, click the *Add Database* button. Horizon Reports Studio then performs the discovery process and adds a new database entry to the data dictionary for the project.