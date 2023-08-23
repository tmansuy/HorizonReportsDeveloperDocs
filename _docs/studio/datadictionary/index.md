---
layout: default
title: Data Dictionary
nav_order: 5
has_children: true
parent: Horizon Reports Studio
---

Horizon Reports is data-driven; it only knows how to query against a particular database if it has information about the database's tables, fields, and relationships. This information is known as "metadata" and is also sometimes referred to as a data dictionary.

![](/assets/images/treeview.png)

The objects defined by the metadata are organized in a tree style list. Objects that have children defined will have an expander arrow visible on the left, which you can use to drill down to the children of that object. 

If you enter text in the *search* box, only items with a name matching the entered text will appear in the treeview. Partial matches work, so you could enter "Customer" in the search to display all tables and fields with that text somewhere in the name. 

When an object in the metadata (a database, table, or field) is updated, the date and time the update was performed is stored. You can enter a date and time in the *Show items updated on or after* section to filter the list of objects in the tree. Only objects that have been updated after the entered date and time will be visible in the list if this is used. If you refresh a project or a database, you can use this setting to show only objects that were modified in some way by the refresh operation.

By default, only the names of the objects are displayed in the tree list, but you can also display the friendly captions as well. Turn on the *Show captions after object names* option to do this. 

Use the *Show objects marked non-reportable* to toggle the display of items that have the *Reportable* setting turned off. 