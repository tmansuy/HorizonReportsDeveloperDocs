---
layout: default
title: BeforeSQLStatementSendToDatabase
nav_order: 13
parent: Report Engine
grand_parent: Plugins
---

The BeforeSQLStatementSentToDatabase method executes after the connnection to the database has been opened but before the SQL statement is sent to the database. This allows you to change something about the connection or send a command to the database before the SQL statement is sent.

## Syntax
```csharp
public void BeforeSQLStatementSentToDatabase(System.Data.IDbConnection conn)
```

## Parameters
*conn*
The connection object being used.

## Return value
None.

## Example
Here's an example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, that sends "SET ANSI_PADDING OFF" to the database so it ignores spaces at the end of strings.

```csharp
/// <summary>
/// Executes after the connnection to the database has been opened but
/// before the SQL statement is sent to the database. In this case, we
/// execute SET ANSI_PADDING OFF so the database engine ignores spaces
/// at the end of strings.
/// </summary>
/// <param name="conn">
/// The connection object being used; the connection has been opened.
/// </param>
public void BeforeSQLStatementSentToDatabase(IDbConnection conn)
{
    IDbCommand cmd = conn.CreateCommand();
    cmd.CommandText = "set ansi_padding off";
    cmd.ExecuteNonQuery();
    cmd.Dispose();
}
```
