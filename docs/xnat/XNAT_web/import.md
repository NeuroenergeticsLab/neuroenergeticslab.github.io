---
layout: default
title: Import Data
parent: XNAT web manual
grand_parent: Data Pipeline
nav_order: 4
---

## Import files from XNAT.
Users can download image session data from XNAT in a variety of contexts: 
- Users can download scan files from any image session on a project report page by selecting Download Images from the actions menu 
- Users can download scan files from an individual session report page by selecting Download > Download Images from the actions menu. 
- Users can download scan files from any data table containing image sessions (for example, by clicking Browse > Data > MR Sessions in the top navigation) by selecting Options > Download in the data table menu 

 Using any of these mechanisms will bring the user to the download UI in the XNAT webapp. Depending on how many sessions you are downloading, 
 or how granular you want to get concerning which scan or resource files to download, you may consider writing a download script that uses the 
 XNAT REST API instead 
 
### Download Image Session from XNAT UI
The Download Sessions UI consists of a single-screen wizard that walks you through the steps of the process. 
- Select Sessions to Download From 
- Select Scan Format and Scan Types to Download. If you find duplicated or redundant scan types in this list, you can use the Scan Type Cleanup functions in XNAT to harmonize your scan type definitions and labels 
- Select Download Format. Option 2 will download scan files to your local computer as a single compressed zip. The Catalog XML option is only used if you want to generate an XML download script for an external application to run 

![image](https://user-images.githubusercontent.com/40626584/200135564-25bf54e9-9344-424d-82e1-e431de5fcb4a.png)

### Downloading imaging file
After clicking Submit, a modal like the one above will come up and inform you of the file to be downloaded. 
If you wish to begin the download, simply click Download. You may then get a pop-up asking whether 
you want your browser to save or open the file you’re downloading. After you make your selection and the file downloads, 
you can view the downloaded file. The file name will match the listed download ID, so ‘test-20201127_124746’ is the name of the file that was saved in. 
XNAT also provides you with the total size of the files to be downloaded (before compression). 
If you are downloading the catalog XML, the extension will be ‘.xml’. 

![image](https://user-images.githubusercontent.com/40626584/200135673-9d2057e4-70be-4f01-8a81-490dcbe038e2.png)


