---
layout: default
title: Migrating from an earlier version
nav_order: 2
parent: Configuring IIS
grand_parent: Deploying Horizon Reports
---

## Backup
It's a good idea to make a complete backup of the contents of the web site folder before beginning the migration process, just in case you want to revert to the previous version.

## Web.config
Custom "appsettings" in web.config are no longer supported. Previously defined settings in web.config need to be moved to [options.json]({% link _docs/how-to/configuring.md %})

## Application pool
The web application no longer supports using a shared application pool. If you previously hosted with a shared pool, create a new [dedicated application pool]({% link _docs/deploying/configuring-iis/index.md %}).

## Migrating existing data and settings
It's recommended to migrate to a new application folder for this release. Once you create the new folder, make sure to set up the permissions as discussed in [Configuring IIS]({% link _docs/deploying/configuring-iis/index.md %}).
The **App_Data**, **Project_Data**, and **Licenses** folders contain all the files that should be migrated to the new release. 

![](/assets/images/remainingfolders.png)

After this, continue publishing to the new application folder as discussed in the [Publishing Horizon Reports]({% link _docs/deploying/publishing.md %}) help topic.

## Plugins

If you have existing plugins, they must be recompiled for .NET 6. If you aren't sure how to do this, you can consider using the [Automatic Compilation]({% link _docs/plugins/automatic-compilation.md %}) feature.
