---
layout: default
title: Administration
parent: Setup
grand_parent: XNAT / Jupyter
nav_order: 2
---

*This first section was copied from [here](https://wiki.xnat.org/display/XW2/Part+2%3A+XNAT+Administration).*

This practical exercise will take you through the most common XNAT Administration tasks associated with setting up projects. Most importantly in this process, we will be setting up channels for properly importing and anonymizing image data from scanners, and routing them to your projects. We will also spend some time on configuring data structure in your project, and uploading custom data resources.

This practical session breaks XNAT Administration and Project Setup into the following steps:
1. [Step 1 of 8: Create New Project](https://wiki.xnat.org/display/XW2/Step+1+of+8%3A+Create+New+Project)
2. [Step 2 of 8: Enable the XNAT DICOM receiver (Note: use port defined in page Installation, step 2b)](https://wiki.xnat.org/display/XW2/Step+2+of+8%3A+Enable+the+XNAT+DICOM+receiver)
3. [Step 3 of 8: Configure DICOM project routing](https://wiki.xnat.org/display/XW2/Step+3+of+8%3A+Configure+DICOM+project+routing)
4. [Step 4 of 8: Write Anonymization Scripts](https://wiki.xnat.org/display/XW2/Step+4+of+8%3A+Write+Anonymization+Scripts)
5. [Step 5 of 8: Configure Series Import Filters](https://wiki.xnat.org/display/XW2/Step+5+of+8%3A+Configure+Series+Import+Filters)
6. [Step 6 of 8: Create a Custom Variable Set](https://wiki.xnat.org/display/XW2/Step+6+of+8%3A+Create+a+Custom+Variable+Set)
7. [Step 7 of 8: Add a Project Resource Uploader](https://wiki.xnat.org/display/XW2/Step+7+of+8%3A+Add+a+Project+Resource+Uploader)
8. [Step 8 of 8: Configure Protocol Validation](https://wiki.xnat.org/display/XW2/Step+8+of+8%3A+Configure+Protocol+Validation)

***

# Test DICOM server
1. Send a test dataset to the location configured in the step (2) of the Administration section. For the automatic mapping of the dataset to an existing project, add the following information to the comments of the study:
`Project:Project_ID` (or Project Alias will work as well) `Subject:Subject_ID` `Session:Session_ID`
2. Check [this page](https://wiki.xnat.org/documentation/how-to-use-xnat/image-session-upload-methods-in-xnat/how-xnat-scans-dicom-to-map-to-project-subject-session) for more information
3. To check the status of the image transmission:
    3. Go to the web interface
    3. Click on **Upload** (Top bar) &#8594; **Go to prearchive**
4. When the status of the study is Ready (refresh the website to check for updates of the status):
    4. Select the study by clicking in the checkbox
    4. Click on **Change projects**
    4. Select the project to which this project belongs to and click on **Ok**
    4. Reload the website, check the study like in (1) and click on **Review and Archive**
    > ![step 4](/pics/1.png)
5. Edit the information and click on **Submit**
    > ![step 5](/pics/2.png)
6. To check the uploaded study click on **Browse** &#8594; **My project** &#8594; **Test project** and select the subject id and session
    > ![step 6.1](/pics/3.png)
    > ![step 6.2](/pics/4.png)

