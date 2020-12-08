---
layout: default
title: Installation
parent: Setup
grand_parent: XNAT / Jupyter
nav_order: 1
---



1. Clone the xnat-docker-compose repository either directly from xnat:
    - `git clone https://github.com/NrgXnat/xnat-docker-compose`
    or the one provided by the Monash Biomedical Imaging group (recommended):
    - `git clone https://github.com/MonashBI/xnat-docker-compose`
2. Edit the docker-compose.yml file:
    - Map the /data/xnat folder to a local folder in the host by editing the volumes section on the xnat-web service. If you cloned the MBI repository (1b), it is recommend to set both environment variables `$DATA_DIR` and `$APP_DIR` to the same location for an easy debugging of the Container service
    - Add the port that will be used as a DICOM listener to the ports section on the xnat-web service (e.g. 8104:8104)
3. Create the folder home/plugins into the host xnat-data folder mapped in (2a) and add the plugins **Container Service** and **XNAT-OHIF** Viewer from the xnat tools website
4. Run Xnat by typing in the terminal:
    - `cd xnat-docker-compose`
    - `docker-compose up -d`
5. Check that it ran without error typing in the terminal:
    `docker-compose logs -f --tail=20 xnat-web`



<br/>
- [x] You are now ready to get started!