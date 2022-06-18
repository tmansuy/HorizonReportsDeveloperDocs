---
layout: default
title: Refreshing the Data Dictionary
nav_order: 9
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

When the structure of a database changes, such as when a new table or field is added, the data dictionary must be updated or the user won't be able to report on the new fields (or worse, if a field was removed or renamed, they'll get an error when they select the old field for a report). To refresh the data dictionary, click the Refresh button (![](/assets/images/refresh.png)). In the Refresh settings dialog that appears, you have the following options:

* *Include views*: Turn this setting on if you want views included in the discovery.

* *Create virtual tables from stored procedures*: With this option on, Studio creates virtual tables for any stored procedures in the database. 

* *Create subtables for self joined tables*: Turn this option on to automatically create a subtable any time any self-joined table or more than one relationship between the same set of tables is discovered. You can rename the subtable if you wish. See the [Creating a Subtable]({% link _docs/studio/datadictionary/table-properties.md %}) topic for information on subtables.

* *Version*: the version number to assign to new tables and fields.

Clicking the *Refresh* button causes Studio to scan the data source and refresh the data dictionary as necessary, adding new tables and fields, changing data types and column widths, and so forth.

If you have certain tables you want ignored when you refresh a database, turn on their *Do not refresh* property.
