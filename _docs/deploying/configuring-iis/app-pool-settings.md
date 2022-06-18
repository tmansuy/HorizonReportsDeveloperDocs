---
layout: default
title: Application Pool Settings
nav_order: 3
parent: Configuring IIS
grand_parent: Deploying Horizon Reports
---

In most cases, the default application pool settings work fine with Horizon Reports. The following settings may need to be changed depending on the behavior you desire.


![](/assets/images/applicationpooladvanced.png)

* *Enable 32-Bit Applications*: In some cases, you might need the web application to run as a 32-bit application. For example, you may needs to access an ODBC DSN defined using the 32-bit DSN manager. In this case, set this option to **True**.

* *Start Mode*: The default for this setting is **On Demand**, which means that the application pool will only start after a request is made. In addition, if the application pool is recycled, it won't automatically restart until a request is made. However, if the scheduler feature is used, the application pool must always be running. If using the scheduler, set *Start Mode* to **AlwaysRunning**.

* *Identity*: This setting allows you to specify which user account applications in this application pool run under. You can create a specific user account on the server and specify that account for this setting or you can use one of the special accounts built into Windows. The default setting of *ApplicationPoolIdentity* is a special case of a built-in account. When you choose this, the actual identity the application pool runs under is created on the fly. If you change this, note what you set it to as you'll need to remember it when setting up folder security.