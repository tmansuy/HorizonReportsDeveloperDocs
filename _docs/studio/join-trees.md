---
layout: default
title: Join Trees
nav_order: 6
parent: Horizon Reports Studio
---

In a complex data dictionary, there may be multiple ways to get from one table to another. For example, in the Sage 300 accounting system:

* OESHDT is related to OESHHD and ICCATG
* OESHHD is related to ICITEM
* ICCATG is related to ICITEM

If a report contains only fields from OESHDT and ICITEM, the correct path is OESHDT - OESHHD - ICITEM. However, the report writer may instead choose OESHDT - ICCATG - ICITEM, which won't give the correct results.

The join weight property of a relationship can help you choose the optimum path, but since that's only used for a specific relationship, it can be complicated getting the correct set of join weights to give the desired path under all conditions. That's where join trees help: a join tree allows you to define exactly what set of relationships the report writer should use to get from one table to another.

To create a join tree, choose the *Join Trees* button on the toolbar, then click the Add button (![](images\addbutton.png)).

![](images/JoinTree.png)

In the *Tables* list, choose the tables that you're interested in specifying how to join. The *Joins* list shows all relationships for those two tables. Turn on the check mark for those relationships you want used in the join tree. Double-click a relationship to jump to that relationship in the databases TreeView.

In the image above, you can see that the Customers-Orders, Orders-[Order Details], and Products-[Order Details] relationships were chosen for the Customers - Products join tree. That means when the report writer encounters fields from Customers and Products in a report, it'll automatically use Customers -> Orders -> Order Details -> Products for the joins for the SQL statement for the report. The Name property is automatically assigned as "Table1,Table2" and is simply used for information purposes.