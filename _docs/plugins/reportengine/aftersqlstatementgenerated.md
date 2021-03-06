---
layout: default
title: AfterSQLStatementGenerated
nav_order: 6
parent: Report Engine
grand_parent: Plugins
---

AfterSQLStatementGenerated is called after the SQL statement needed to retrieve the report's data has been generated but before it's sent to the database engine. You can alter the SQL statement as desired.

## Syntax
```csharp
public string AfterSQLStatementGenerated(
    IReport report,
    string sqlStatement,
    object[] parameters,
    string tablename,
    System.Data.IDbConnection conn,
    System.Data.IDbCommand cmd,
    string dataSourceName)
```

## Parameters
*report*
The report being run.

*sqlStatement*
The SQL statement generated by the data engine.

*parameters*
The values of any parameters used in the SQL statement.

*tableName*
The name of the data table being created.

*conn*
The connection object being used.

*cmd*
The command object being used.

*dataSourceName*
The name of the current data source being queried.

## Return value
The SQL statement to be used or null if the SQL statement should not be sent to the database. If the method doesn't alter the SQL statement, return the passed-in value.
