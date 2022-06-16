---
layout: default
title: Configuring the Web Application
nav_order: 3
parent: How To
---

You can configure the following options in an **options.json** file in the root of the web application folder:

- *schedulerconnectionstring*: A connection string for a SQL Server database to use for the scheduler. Only specify this if running Stonefield Query Enterprise in [Clustered Mode](vfps://Topic/_6010qs8m6)
```json
{
    "schedulerconnectionstring": "Data Source=dbserver;Initial Catalog=SQSchedules;uid=sa;pwd=sapassword"
}
```
- *cacheconnectionstring*: A connection string for a SQL Server database to use as system cache. Only specify this if running Stonefield Query Enterprise in [Clustered Mode](vfps://Topic/_6010qs8m6)
```json
{
    "cacheconnectionstring": "Data Source=dbserver;Initial Catalog=SQDistCache;uid=sa;pwd=sapassword"
}
```
- *logintimeout*: The inactive time in minutes before a user is automatically logged out. The default setting is 20 minutes. This means that if a user closes their browser without logging out, it will take 20 minutes for the the license occupied by that user to be freed for use with another user.
```json
{
    "logintimeout": 20
}
```


## Options.json example
Here is an example of an options.json file with all configuration options specified

```json
{
    "cacheconnectionstring": "Data Source=dbserver;Initial Catalog=SQDistCache;uid=sa;pwd=sapassword",
    "schedulerconnectionstring": "Data Source=dbserver;Initial Catalog=SQSchedules;uid=sa;pwd=sapassword"
    "logintimeout": 5,
    "project": "C:\\MyProjects\\Northwind\\Project_Data\\settings.xml",
    "appsettings": "C:\\MyProjects\\Northwind\\App_Data\\applicationsettings.xml"
}
```

You can configure the following options in an **hrsettings.json** file in the root of the web application folder:

- *DefaultConnectionString*: A connection string for a database that stores the projects for this installation. 
```json
{
    "DefaultConnectionString": "Data Source=Project_Data\\horizonreports.db"
}
```
- *ConnectionType*: The type of database that stores the projects. SQLite, SqlServer, and MySql are supported options.
```json
{
    "ConnectionType": "SQLite"
}
```
- *CurrentProject*: The database ID of the project to load in the report writer. Normally you would change this value in the Horizon Reports Studio interface. 
```json
{
    "CurrentProject": 1
}
```