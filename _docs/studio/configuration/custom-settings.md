---
layout: default
title: Custom Settings
nav_order: 3
parent: Configuration
grand_parent: Horizon Reports Studio
---

Your [plugins]({% link _docs/plugins/index.md %}) may need additional settings that can be configured for the user. Custom settings also may be needed as parameters for reports. To define these settings, use the Custom Setting tab in the Configuration section of Studio.

To create a custom setting, click the Add button (![](images\addbutton.png)).

![](/assets/images/CUSTOMSETTINGS.PNG)

A custom setting has the following properties:

* *Name*: the name of the setting. Names must follow typical naming rules: only letters and number and it must start with a letter.

* *Caption*: the caption for the setting as it should appear to the user in a dialog.

* *Type*: the data type for the setting's value. The choices are String, Int, DateTime, Double, and Bool.

* *Default value*: the default value for the setting.

To use a custom setting in a plugin, use code like the following:

```csharp
var settingValue = Application.Configuration.Users[
    Application.Security.CurrentUser.Name]
    .CustomSettings["SettingName"];
```

where "SettingName" is the name of the setting.

To use a custom setting in a report template, edit the template using the Template Editor and add a parameter with the same name as the custom setting and its Visible property set to false (unless you want the user to be able to edit the value in the preview window). Add a label to the template that is data-bound to the new parameter (see the end-user help for details on using the Template Editor and data binding).