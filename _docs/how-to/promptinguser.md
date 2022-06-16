---
layout: default
title: Prompting the User for Values
nav_order: 11
parent: How To
---

Although Horizon Reports can prompt the user for values of ask-at-runtime conditions, there may be other cases where you want to prompt the user for a value to be used somewhere. Here are a couple of ways you can do this:

* For stored procedures called from the [Select]({% link _docs/plugins/virtualtable/select.md %}) method of a virtual table, use code in the GetParameters method to specify parameters the user is prompted for when a report using fields from the virtual table is run.

* For a database function that needs to be passed a parameter from user input, use the built-in [GetParameter](vfps://Topic/_16W0VJB34) function as part of the function call to prompt the user for the value. For example, this would be the Expression of a calculated field that calls the MyFunction function, passing it the value entered by the user when prompted:

        dbo.MyFunction(GetParameter("SomeValue", "Enter Some Value", "String", "Default"))