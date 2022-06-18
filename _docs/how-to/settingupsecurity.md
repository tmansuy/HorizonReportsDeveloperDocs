---
layout: default
title: Programatically Setting Up Security
nav_order: 10
parent: How To
---

The Security dialog in Horizon Reports is used to define users and roles and what permissions roles have. However, you can also set up security programmatically if you wish.

First, see the information in the [Using Horizon Reports from Other Applications]({% link _docs/how-to/usingfromotherapps.md %}) topic for details on how to instantiate and set up the Application object. Then you can use code as shown below.

## Adding roles
To add a role, add a Role object to the Security's Roles collection. To save the new role to the Roles, call SaveItem. For example:

```csharp
Role role = _app.Security.Roles["My Role"];
if (role == null)
{
  role = _app.Security.Roles.New["My Role"];
  _app.Security.Roles.SaveItem(role);
}
```

## Adding users
To add a user, add an IUser object to the Security's Users collection. To save the new user to the Users security table, call SaveItem. For example:

```csharp
User user = _app.Security.Users["My User Name"];
if (user == null)
{
  user = _app.Security.Users.New["My User Name"];
  user.Password = "my password";
  user.LicenseType = LicenseType.ReportDesigner;
  Role role = _app.Security.Roles["My Role"];
  user.Roles.Add(role);
  _app.Security.Users.SaveItem(user);
}
```

## Reports
To define the security for a report, add IPermission objects to the report's Permissions collection. For example:

```csharp
Role role = _app.Security.Roles["My Role"];
IReport report = _app.ReportEngine.Reports["My Report"];
report.Permissions.Add(new Permission(role, AccessRights.Full));
```

## Data group
To define the security for a data group, call the data group's AddPermssion method. For example:

```csharp
Role role = _app.Security.Roles["My Role"];
DataGroup dg = _app.DataDictionary.DataGroups["My DataGroup"];
dg.AddPermission(new Permission(role, AccessRights.Full));
```

## Data source
To define the security for a data source, add IRole objects to the data source's Roles collection. For example:

```csharp
Role role = _app.Security.Roles["My Role"];
DataSource ds = _app.ConnectionManager.DataSources["My Datasource"];
ds.Roles.Add(role);
```

## Resources
To define the security for a resource, call the SetResourcePermission method of the Security object. For example:

```csharp
Role role = _app.Security.Roles["My Role"];
_app.Security.SetResourcePermission("TagEditorAccess", role,
    AccessRights.Full);
_app.Security.SetResourcePermission("SchedulerAccess", role,
    AccessRights.Full);
```