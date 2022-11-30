---
layout: default
title: Creating a Relation
nav_order: 8
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

Horizon Reports makes it easy for the end-user: if they select fields from more than one table, they don't have to specify how to join those tables. The data dictionary has information about the relations between pairs of tables, so it determines how to join all the tables involved in the report with that information.

When you add a database to the data dictionary, Studio tries to read information about the relationships between tables from the data source. If the data source doesn't contain any relationship information, either because the database engine doesn't support that information or because the database designer didn't define any relationships in the database, you have to define the relationships between the tables using Horizon Reports Studio.

To create a new relation between a pair of tables, click the Add button (![](/assets/images/addbutton.png)) beside the Relations node in the TreeView for one of the tables.

Select the two tables involved in the relation in the properties pane, as well as the fields involved in the join.
