---
layout: default
title: Overview of architecture
parent: Data Pipeline
nav_order: 1
---

## Overview of our architecture
The architecture at the Neuroenergetics Lab looks like this.

![image](https://user-images.githubusercontent.com/40626584/214580105-a66f0dcf-1049-4cfd-8743-58f49fec18a2.png)

- Davinci is our remote server
  - Once logged in (e.g. with `ssh`), we can access the Docker engine, Jupyter Hub and our RAID storage
- Bratum is the name of the virtual machine running on Davinci
  - XNAT runs inside Bratum
  - We have the `sudo` rights within Bratum
- We use the official [xnat-docker-compose](https://github.com/NrgXnat/xnat-docker-compose) distribuiton
  - Consists of three containers configured by Docker Compose and running on a separate Docker engine on Bratum:
    - **xnat_web** is the web application
    - **xnat_db** is the PostgreSQL database
    - **xnat_nginx** is the proxy
  - XNAT's [Container Service Plugin](https://wiki.xnat.org/container-service/) has connection to the Docker engine running on Davicni
    - Our (high-performace) Davinci server executes all data processing in Docker containers 


XNAT can be accesssed via three different ways. (Click on the corresponding links to connect to xnat now):  
- [XNAT web](https://xnat.tumnic.mgruber.eu/app/template/Login.vm#!). Read about XNAT web [here](https://neuroenergeticslab.github.io/docs/xnat/XNAT_web/)
- ssh connection `<username@xnat.tumnic.mgruber.eu>`
- [Jupyter Hub (requires VPN connection)](http://10.0.4.1:8000/hub/login)

_Note: If you are on Research Network you dont need openVPN for Jupyter Hub connection, otherwise you have to connect._
