---
layout: default
title: Configuring Docker
nav_order: 3
parent: Deploying Horizon Reports
---

Horizon Reports can run in a Linux environment. The best way to do that is with the docker image [horizon-reports](https://github.com/users/tnmsoft/packages/container/package/horizon-reports). 

# Configuring the Docker container

To deploy Horizon Reports using docker, use the *docker run* command. Configuration for the container is done via command line arguments to *docker run*: 

* In order to persist projects and settings, the container requires 2 volume mappings. One for /app/App_Data and one for /app/Project_Data.  

* The containers internal port 80 must be mapped to port on the host. It isn't necessary to map port 443 for SSL/HTTPS connections. Instead, use a reverse proxy configuration for [Nginx](https://nginx.org/en/) or [Apache](https://apache.org/).

The following example *docker run* command will create a container named horizon-reports using the Horizon Reports docker image, bound to port 8000, and using 2 named docker volumes called *appdata* and *projdata*:


```console
docker run -d --restart=always -p 8000:80 -v appdata:/app/App_Data -v projdata:/app/Project_Data --name horizon-reports ghcr.io/tnmsoft/horizon-reports:latest
```