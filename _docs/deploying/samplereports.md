---
layout: default
title: Providing Sample or Standard Reports
nav_order: 2
parent: Deploying Horizon Reports
---

If you want to supply some sample or standard reports, create them with a local installation of Horizon Reports and copy the SFX files into the Project_Data\StockReports folder (create this folder if necessary). When you [publish]({% link _docs/deploying/publishing.md %}) your project, these reports are automatically imported and added to the set of reports in App_Data\Reports the next time the report writer is started. If you make any changes to the SFX files in the StockReports folder, such as if you update a report and copy the SFX file to that folder, the changes are automatically propagated.

If you don't want users to modify or delete these reports, be sure to change the Access setting for the Everyone role in the Security step of the report wizards to "Read."