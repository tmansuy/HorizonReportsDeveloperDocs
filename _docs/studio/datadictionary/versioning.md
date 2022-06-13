---
layout: default
title: Versioning
nav_order: 10
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

Horizon Reports supports versioning of data dictionary objects. This is useful if tables and fields were added to or removed from the database between versions and you have some users using an older version and some using a newer version but they're all using the latest version of your customized report writer. To prevent users from selecting tables and fields that may not exist in their version of the database, you can specify the version number for each table and field that doesn't exist in all versions. The [GetVersion](vfps://Topic/_2E10WACPQ) method of a data dictionary plugin allows you to tell Horizon Reports what version a particular table or field is at in the user's specific database. Tables, fields, and relationships all have a Version property you can fill in manually. You can also specify what version number to assign tables and fields in the [Add Database dialog](vfps://Topic/_0OV0UB5HW) and what version number to use for new tables and fields when you [refresh the data dictionary](vfps://Topic/_0W40YBOER).

Versioning starts with the Version properties of tables, fields, and relationships. A blank value means the object is not versioned: it appears in the report writer regardless of the version of the database. For an object that isn't available in every version of the database, enter the version number followed by "+" to indicate the object appears in that version and higher versions and should not appear in lower versions (that is, the object was added in that version), "-" to indicate the object appears in that version and lower versions and should not appear in higher versions (that is, the object was removed in the next version), or no suffix to indicate the object appears only in that version and should not appear in any other version. For example, "5.3+" indicates the object is available starting in version 5.3 while "5.3-" indicates it was removed in version 5.4.

The next step is telling the report writer which version a particular table, field, or relationship is in the user's selected database. You do this by creating a data dictionary plugin with three [GetVersion](vfps://Topic/_2E10WACPQ) methods, one for fields, one for tables and one for relationships. These methods are passed references to the object in question. The code for these methods should determine what version the specified object is in the user's selected database and return that version number as a string. The reason these methods are called for individual tables, fields, and relations rather than the database as a whole is that some applications have different versions for different objects. For example, someone may be using Version 5.5 of the Accounts Receivable module but version 5.4 of the General Ledger. If your application doesn't have separate version information for different data objects but just one for the entire database, you can have all three GetVersion methods call a common method that returns the version number. See the [GetVersion](vfps://Topic/_2E10WACPQ) topic for some sample code.

Here's how this works: when a table, field, or relationship that has a non-blank Version property is accessed in the data dictionary, such as displaying a list of tables in the Report Wizard, the report writer calls GetVersion for that item and compares the two versions. It prevents access to the item (acting as if it doesn't exist in the data dictionary) if:

* the data dictionary version number has a "-" suffix (meaning the object is available in the specified version or earlier versions) and the database version number is greater than the data dictionary version number;

* the data dictionary version number has a "+" suffix (meaning the object is available in the specified version or later versions) and the database version number is less than the data dictionary version number; or

* the data dictionary version number has a no suffix (meaning the object is available only in the specified version) and the database version number is different than the data dictionary version number

Thus users cannot select tables and fields that don't exist in their selected database when they create a report.