---
layout: default
title: Multi-Tenant Support
nav_order: 12
parent: Horizon Reports Studio
---

Many web applications are multi-tenant, meaning a single instance of the software serves multiple clients, called tenants. When a user logs into the application, they only see records created by users in the same tenant as they are. This is typically handled using one of two mechanisms:

* Each tenant has their own database so they only have access to the records in that database. The application connects to the appropriate database when a user retrieves or updates records.

* All tenants share a database, but each table has a certain field containing an ID indicating which tenant the record belongs to. When the user adds a record, that field is filled in with the appropriate value for their tenant, and when they retrieve records, only records with that value in that field are retrieved.

Horizon Reports supports multi-tenant environments if you set the [Support multi-tenant environment]({% link _docs/studio/multi-tenant.md %}) configuration setting to true. Here's how this is supported:

* For administrative users, the Security dialog has a Tenants tab in which you can manage tenants: the tenant name, which data source users in that tenant connect to (if the [Filter Field for Queries in Multi-Tenant]({% link _docs/studio/configuration/configuration-settings.md %}) configuration setting is blank), and the ID value for the tenant (if that configuration setting isn't blank). Also, the Users and Roles tabs of the Security dialog have Tenant settings where you can assign a tenant to users and roles.

* You can assign the Tenant Administrator role to a user. Users in this role have access to the Security dialog but they don't see the Tenants tab, the Users and Roles tabs only show users and roles for the tenant they're in, and any users and roles they add are automatically assigned to their tenant. This allows someone at the client to manage the users who can access the report writer.

* If the *Filter field for queries in multi-tenant* setting is blank, meaning the first mechanism discussed above is used, when the user runs a report, Horizon Reports automatically connects to the data source for the tenant the current user belongs to as specified in the Tenants tab of the Security dialog.

* If the *Filter field for queries in multi-tenant* setting is filled in, meaning the second mechanism discussed above is used, Horizon Reports automatically adds a condition of "*field* = *value*" to the WHERE clause of every SQL statement it sends to the database, where *field* is the name of the field specified in that setting and *value* is the ID for the tenant the current user belongs to as specified in the Tenants tab of the Security dialog.

* For administrative users, the Tag Editor and the report wizards have a Tenant setting where you can select the tenant that can access the tag or report.

* Any tags or reports created by non-administrative users are automatically assigned to the tenant the user is in.

* Users can only see tags, reports, and formulas assigned to the tenant they belong to.

* When the Tenant Administrator uses the Upload a Logo Image function in the Tools menu, the image file uploaded is specific for that tenant. When a user belonging to that tenant runs a report using a template with a logo, such as Professional - Blue with Logo, the tenant-specific image is used in the report.

So, the bottom line is that users can only see things&mdash;database records, tags, formulas, and reports (and other users and roles in the case of Tenant Administrators)&mdash;that belong to their tenant. No custom plugins are required for this behavior; it's built-in and controlled with just a few configuration settings.