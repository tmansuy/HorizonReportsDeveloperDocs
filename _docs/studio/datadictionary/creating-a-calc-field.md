---
layout: default
title: Creating a Calculated Field
nav_order: 7
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

Like a virtual table, a calculated field doesn't physically exist but is defined only in the data dictionary. For example, most order entry systems don't store the extended price of an item, but derive it from the unit price multiplied by the quantity. However, you may want your users to be able to report on extended price, so you would create a calculated field for it. 

To create a calculated field for a particular table, click the Add button (![](/assets/images/addbutton.png)) beside the Calculated Fields node in the TreeView for that table. 

Enter the various properties for the field in the Main page of the properties pane, and in the Calc pane, enter the formula used to calculate the value for the field in the Expression property.
