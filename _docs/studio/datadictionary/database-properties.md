---
layout: default
title: Database Properties
nav_order: 2
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

When you select a database in the treeview, an editor displays the properties for that database.

A database defined in the data dictionary is a logical database: it defines what tables belong to the database and the structure of those tables. A physical database is the actual database on disk. The logical database doesn't concern itself with connection information; those are issues for the physical database. For example, you may have both SQL Server and Microsoft Access versions of the same logical database; the Northwind sample database that comes with both of these is one such set of physical databases that have the same logical database structure.

Some applications have more than one database. This is especially true if you want to use Horizon Reports to integrate the data of several applications. For example, imagine an accounting application that has two databases: a system database that contains application-specific data, and a company-specific database containing the accounting information for the company. The user may have different databases for different companies, so they can change data sources to select the appropriate database for the desired company. However, there is only one system database.

The properties displayed are:

![](images\databaseprops.png)

* *Name*: the name of the database. Note that this is the logical name of the database, not the physical name. You cannot edit the name.

* *Order*: the order in which this database is accessed. The lower the number, the earlier it is accessed.

* *Name delimiters*: this specifies which characters to use as delimiters around table and field names that need delimiters (for example, names with spaces in them). Specify a two-character value, with the first character being the left delimiter and the second being the right. Examples are "", meaning use double quotes, and [], meaning names are delimited with square brackets. MySQL needs the reverse apostrophe: ``; in fact, if specify something other than the reverse apostrophe, you are asked whether you wish to use the reverse apostrophe instead.

* *Active*: if this setting is turned off, the database and its tables do not appear in the report writer.

* *Version*: the database's [version number](vfps://Topic/_2M70UOIFZ). A blank value means the database is not versioned: it appears in the report writer regardless of the version of the application. For a database that isn't available in every version of the application, enter the version number followed by "+" to indicate the database appears in that version and higher versions and should not appear in lower versions (that is, the database was added in that version), "-" to indicate the database appears in that version and lower versions and should not appear in higher versions (that is, the database was removed in the next version), or no suffix to indicate the database appears only in that version and should not appear in any other version. For example, "5.3+" indicates the database is available starting in version 5.3 while "5.3-" indicates it was removed in version 5.4.

    Use a comma-delimited list of values if the database was added in one version and later removed. For example, "5.3+,5.5-" means it was added in version 5.3 and removed in version 5.6.

    Versioning isn't commonly used with databases; it is more frequently used with fields and tables.

* *Connection type*: the type of connection to use to connect to the database in the report writer (not in Studio). The options are:

    * *Use default connection*: this means the same connection information is used for both Studio and the report writer: the connection string displayed in the *Connection string* setting discussed later.

    * *Share connection*: if this item, which is only available when there's more than one database in the data dictionary and when *Order* is greater than 1, is turned on, this database shares its connection information with the database chosen in the *Share with* setting. In that case, the name of the database in the data dictionary is used as the physical name when connecting to the database.

    * *User can choose DSN*: this choice means the end-user can choose which physical database to connect to by selecting a DSN from a dialog in the report writer.

    * *Scripted*: select this if you want to use a plugin to define how to connect to the database. This option provides the most flexibility because, for example, you can use the same run-time connection settings your main application uses. See the [GetDataSources](vfps://Topic/_0OV0TGF6C) topic for details on a database connection plugin.

    * *User can manage connection string*: this allows you to define the connection string for the database at runtime (in the Setup Wizard) without having to create a plugin to set the connection string. The connection string is stored in the encrypted datasources.xml file in the App_Data folder. This file should not be deployed to the web server but is created there the first time Horizon Reports is run.


* *Connection string*: this contains the connection string to use when refreshing the data dictionary in Studio or in the report writer when *Connection type* is set to *Use default connection*. To use a DSN, specify "dsn=*DSN name*." For ODBC, the connection string is typically something like "driver=*ODBC driver name*;server=*server name*;database=*database name*;uid=*user name*;pwd=*password*." For OLE DB, the connection string is typically something like "Provider=*OLE DB provider name*;Data Source=*server name*;Initial Catalog=*database name*;User ID=*user name*;Password=*password*." For SqlClient, the connection string is typically something like "Provider=System.Data.SqlClient;Server=*server name*;Database=*database name*;User ID=*user name*;Password=*password*." See <a href="http://www.connectionstrings.com" target="top">www.connectionstrings.com</a> for connection strings for different ODBC drivers and OLE DB providers.

* *Test*: click this button to test the connection settings for the database.

* *Custom properties*: Horizon Reports doesn't use this property for anything. You can use it to hold any information you wish. The value is stored in the UserDefined property of the Database object, which a [plugin]({% link _docs/plugins/index.md %}) could use for any purpose necessary.

