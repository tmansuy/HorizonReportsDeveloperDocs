---
layout: default
title: Clustered Mode
nav_order: 4
parent: Configuring IIS
grand_parent: Deploying Horizon Reports
---

Horizon Reports can run in *Clustered* mode if running in a [Web Farm](https://docs.microsoft.com/en-us/iis/web-hosting/scenario-build-a-web-farm-with-iis-servers/configure-a-web-farm-with-iis-servers). Additional configuration is necessary when running in *Clustered* mode.

> All servers in a cluster must have synchronized clocks. Made sure to use some form of time-sync service on each server in the cluster.

## SQL Server
Two SQL Server databases are needed for *Clustered* mode.

### Cache
A SQL Server database to use for caching is required for proper operation in a clustered environment. If you haven't already created a caching database, use the **dotnet sql-cache create** command. For example:
```
dotnet sql-cache create "Data Source=dbserver;Initial Catalog=SQDistCache;uid=sa;pwd=sapassword" dbo SQWebCache
```

Once the caching database has been created, configure *CacheConnectionString* in [options.json]({% link _docs/how-to/configuring.md %}).

### Scheduler

A SQL Server database is required for the scheduler. If you haven't already done so, create a SQL Server server database for the scheduler, then configure *SchedulerConnectionString* in [options.json]({% link _docs/how-to/configuring.md %}).

# ARR and IIS

Horizon Reports requires sticky sessions when running in a clustered environment. If you're using ARR (Application Request Routing) with IIS, you can enable sticky sessions by doing the following:

- On the ARR server, open IIS Manager
- Under Server Farms, select the server farm entry for Horizon Reports
- Double click the "Server Affinity" icon
- Turn on the "Client affinity" option. Though it isn't necessary, it's recommended that you provide a unique "Cookie name" value.
