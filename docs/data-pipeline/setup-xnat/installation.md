---
layout: default
title: Installation
parent: Setup XNAT
grand_parent: Data pipeline
nav_order: 1
---



1. Clone the xnat-docker-compose repository either directly from xnat into your server. *Open the default.env file and note the Time zone (TZ) and the version of the xnat. This will be useful when you would need to install the compatible versions of the plugins.
    - `$git clone https://github.com/NrgXnat/xnat-docker-compose`
    -  `$cd xnat-docker-compose`.
    
2. Set Docker enviroment variables: Default and sample enviroment variables are provided in the default.env file. Add these variables to your environment or simply copy default.env to .env . Values in this file are used to populate dollar-notation variables in the docker-compose.yml file.
    - `$cp default.env .env`
  
3. Configurations: The default configuration is sufficient to run the deployment. The following files can be modified if you want to change the default configuration 
    - **docker-compose.yml**: How the different containers are deployed. There is a section of build arguments (under `services → xnat-web → build → args`) to control some aspects of the build.
        - If you want to download a different version of XNAT, you can change the `XNAT_VERSION` variable to some other release.
        - The `TOMCAT_XNAT_FOLDER` build argument is set to `ROOT` by default; this means the XNAT will be available at `http://localhost`. If, instead, you wish it to be at `http://localhost/xnat` or, more generally, at `http://localhost/{something}`, you can set `TOMCAT_XNAT_FOLDER` to the value something.
        - If you need to control some arguments that get sent to tomcat on startup, you can modify the `CATALINA_OPTS` environment variable (under `services → xnat-web → environment`).
    - **xnat/Dockerfile**: Builds the xnat-web image from a tomcat docker image.


4. Run Xnat by typing in the terminal:
    - `docker-compose up -d`
5. Check that it ran without error typing in the terminal:
    `docker-compose logs -f --tail=20 xnat-web`



<br/>
- [x] You are now ready to get started! *More info about the Environment variables can be found at [link](https://github.com/NrgXnat/xnat-docker-compose)*
