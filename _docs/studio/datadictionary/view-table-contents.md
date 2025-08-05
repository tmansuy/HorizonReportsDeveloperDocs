---
layout: default
title: Viewing Table Contents
nav_order: 12
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

You can use Studio to retrieve the data for a table. To do so, use the action icon in the right hand column of the database list that appears for table entries.

![](/assets/images/viewtablemenu.png)

After the contents of the table are retrieved from the database, they appear in a dialog. 

![](/assets/images/tablecontents.png)

If any of the columns defined for the table cause an error when executing the query, the retrieval will be tried again without the columns with errors. Any columns that initially generated an error will have their contents filled with "Error".