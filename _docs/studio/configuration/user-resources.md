---
layout: default
title: User Access Resources
nav_order: 2
parent: Configuration
grand_parent: Horizon Reports Studio
---

The Security dialog of the report writer allows an administrative user to define which features the members of the role have access to. For example, it allows specifying that members can edit the properties of the fields in a report but not add or remove fields.

The User Resources section of the configuration lists the resources which can be configured in the report writer and allows you to determine what the default access is. Normally, *Allow default access* is turned on but, for example, if you want access to the Tag Editor restricted to administrative users by default, select the Scheduler resource and turn *Allow default access* off.

The built-in resources you can change the default access to are:

* *ChangePassword*: this controls whether users can access the Change Password function in the Tools menu.

* *Formulas*: this controls whether users can access the Formulas function in the Tools menu.

* *ImportExport*: the controls whether users can import and export reports.

* *Options*: this controls whether the user can access the Options function in the Tools menu.

* *ReportPreviewExport*: this controls whether users can export reports in the Preview window.

* *ReportPreviewPrint*: this controls whether users can print reports in the Preview window.

* *ReportWizardFieldMembership*: this controls whether users can add fields to or remove fields from a report.

* *ReportWizardFieldProperties*: this controls whether users can change the properties of fields in a report.

* *ReportWizardFiltering*: this controls whether users can edit the filter conditions for a report.

* *ReportWizardGeneralOptions*: this controls whether users can change the options in step 5 of a report wizard.

* *ReportWizardGroupingSorting*: this controls whether users can change the grouping or sorting of a report in step 3 of a report wizard.

* *ReportWizardInformation*: this controls whether users can change the settings in step 1 of a report wizard.

* *ReportWizardRoles*: this controls whether users can change the security settings of a report in step 6 of a report wizard.

* *Scheduler*: this controls whether users can schedule a report or change the settings for schedules.

* *TagEditor*: this controls whether users can access the Tag Editor.


You can also add new resources to appear in the report writer Security dialog. New user access resources won't affect the report writer, but allow you to control access to features from plugins.

To add a new user access resource, click the Add button (![](images\addbutton.png)).