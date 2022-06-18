---
layout: default
title: Security
nav_order: 10
parent: Horizon Reports Studio
---

Horizon Reports has multiple levels of security.

The first level is login security. If the user does not have a valid user name and password, they cannot log into the report writer and therefore cannot run any reports.

The next set of levels are role-based. The administrator of can create users and roles in the Security dialog (available from the Tools menu) and assign a user to one or more roles. All users are automatically a member of the Everyone role.

For example, if Mary is a member of both the Administrator and Manager roles, she can access both the Security dialog and any reports available only to members of Manager. If Bob is a member of the Clerk role, he cannot access the Security dialog (a user has to be a member of the Administrator role for that) or any reports available only to members of Manager, but can access any reports available to Everyone and those available only to members of Clerk.

Roles are used in several ways:

* In the Security dialog, an administrator can specify which roles can access certain [data groups]({% link _docs/studio/creating-a-data-group.md %}) (this isn't available if you haven't defined any data groups in Studio). If a role doesn't have rights to a particular data group, none of the users in that role has access to any of the tables in that data group. Those tables won't show up in the report wizards and if the user selects a report containing one of the tables, they get an error message that the report contains tables or fields they do not have access to.

* You can specify which roles have access to certain tables and fields in Studio. See the [Table Properties]({% link _docs/studio/datadictionary/table-properties.md %}) and [Field Properties]({% link _docs/studio/datadictionary/field-properties.md %}) topics for details. As with data group access, tables and fields the user can't access don't show up in the report wizards and if the user selects a report containing one of the tables or fields, they get an error message that the report contains tables or fields they do not have access to.

* When a report is created or edited, the user can specify which roles have access to the report in the Security step of the report wizards. By default, a report is available to the Everyone role, but the user can remove that role and add a different role (such as Managers) to make the report available to only users in that role. If no roles have access to the report, the report is essentially private, available only to its creator. In addition to specifying which roles have access, the user can specify what rights members of the role have: only the ability to run the report or the ability to edit or delete it.

If a user is a member of more than one role, their rights are ORed when determining their access to a particular report, folder, table, or field. For example, suppose John is a member of the Manager and Clerk roles. Members of Manager have access to the Payroll table but members of Clerk do not. Members of Clerk have access to the Products report but members of Manager do not. In that case, John has access to both the Payroll table and the Products report, since he is a member of roles with access to those items.


