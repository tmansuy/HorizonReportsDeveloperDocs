---
layout: default
title: AfterLogin
nav_order: 1
parent: Application
grand_parent: Plugins
---

The report writer calls the AfterLogin method of any application plugin after the user logs in. This can be used for any user-specific set up code.

## Syntax
```csharp
public bool AfterLogin(IUser user)
```

## Parameters
*user*
A reference to the logged-in user.

## Return value
True if the application should continue, False if it should terminate.
