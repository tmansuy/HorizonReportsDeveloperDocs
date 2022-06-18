---
layout: default
title: Creating a Data Group
nav_order: 7
parent: Horizon Reports Studio
---

If your application database has a lot of tables, you may wish to group them. For example, an accounting application may have different modules, such as General Ledger, Accounts Payable, and Accounts Receivable. Rather than making the user select from hundreds of tables in the Step 2 of the report wizards, if you group your tables, they can select which data group they want to work with in Step 1, and then only see the tables in that group in Step 2 (they can also choose to see all tables).

A table can belong to more than one data group. For example, the Customers table in an accounting system might belong to the Accounts Receivable data group, but also the Order Entry data group. Place a table in as many data groups as makes sense for your users.

Data groups can also be used for security purposes; the Security dialog (available from the Tools menu in Horizon Reports) allows an administrator to restrict access to certain data groups on a role-by-role basis.

The phrase "data group" can be replaced with one that is more meaningful to your users if you wish, such as "module." See the [Multi-Language Support]({% link _docs/studio/multi-language.md %}) topic for information on how to do that.

Before you can select which data groups a table belongs to, you have to define some. To add a data group, choose the *Data Groups* button on the toolbar, then click the Add button (![](/assets/images/addbutton.png)).

![](/assets/images/datagroups.png)

After creating a data group, enter the name for the group. Since these names are only used internally in the report writer and not for queries against the database, you don't have to worry about delimiters for names containing spaces or other characters. You are not allowed to leave the name blank or enter a duplicate name. Next, define the default table for the data group. When the user selects the data group in Step 1 of a report wizard, the table you specify in the *Default table* setting is automatically selected for a new report in Step 2.

You can define the [default data group]({% link _docs/studio/configuration/configuration-settings.md %}) for new reports if you wish. When the user creates a report, that data group is selected by default in the report wizards.

