---
layout: default
title: Publishing Horizon Reports
nav_order: 2
parent: Deploying Horizon Reports
---

# Publishing a Project
To deploy Horizon Reports on a web server, you need to deploy two things:

- Horizon Reports web application: On the web server, download the [web application installer](https://www.horizon-reports.com/downloads/current/hrwebsetup.exe) and install. The application requires the [ASP.NET Core 8.0 Hosting Bundle](https://download.visualstudio.microsoft.com/download/pr/00397fee-1bd9-44ef-899b-4504b26e6e96/ab9c73409659f3238d33faee304a8b7c/dotnet-hosting-8.0.4-win.exe), but the installer should automatically download and install this. Under linux, you must first have [docker](https://www.docker.com/) installed. Then, use the [horizon-reports-docker](gchr.io) image to create a new container. 

> <span class="glyphicon glyphicon-info-sign" aria-hidden="true"></span> If you're deploying to Azure or similar and are unable to run the installer, instead install to a local folder and then upload the contents of that folder to the server.

- Horizon Reports project: The project files that need to be deployed are contained in the subfolder *Project_Data* of your local Horizon Reports installation. To deploy the project, copy the *Project_Data* folder from your development environment folder to the web application folder. If you're using default settings for the project database (i.e. a SQLite database located in Project_Data), deploying the *Project_Data* folder should also include this database.

> <span class="glyphicon glyphicon-info-sign" aria-hidden="true"></span> If your project database is stored in something other than a SQLite database, you have to install that database yourself.

Regardless of whether the web site is on the current or a remote system, the following settings are required for the web server:

* Enable read and write access to the App_Data, Licenses, and Logs folders.

> <span class="glyphicon glyphicon-info-sign" aria-hidden="true"></span> For docker based deployments, the Licenses and Logs folders will be located under the App_Data shared volume. 

### Publishing to Microsoft Azure
The simplest way to publish to a Microsoft Azure server is to publish to a local folder first, then copy the files from the local folder to the Azure server. Follow these steps:

* Make sure the Remote Desktop Connection (RDP) to connect to the Azure server is configured to allow access to a drive on the local system. To do that, right-click the RDP file and choose Edit from the shortcut menu. Select the Local Resources tab, click the More button, and turn on one or more local drives.

    ![](/assets/images/rdp.png)

* Download the [web application installer](https://www.horizon-reports.com/downloads/current/hrwebsetup.exe) and install to a local folder.

* Copy the *Project_Data* folder from your Horizon Reports installation to the same local folder.

* Double-click the RDP file to connect to the Azure server.

* Create a [new site]({% link _docs/deploying/configuring-iis/index.md %}) using IIS Manager.

* Using Windows Explorer, copy the files from the local publish folder to the virtual directory on the Azure server.

### Publishing to a Microsoft Azure web site
Publishing to a Microsoft Azure web site is straightforward. Follow the steps in the previous section to create a publish folder on a local drive, then upload the contents of that folder to the site using FTP.

### Publishing to a docker container
Follow the steps in the previous section to create a publish folder (Project_Data) on a local drive. Once it's ready, upload the contents of that folder to docker host machine using FTP/SFTP/SCP. When [docker container]({% link _docs/deploying/docker.md %}), make sure to map a shared volume to the publish folder you copied. 

