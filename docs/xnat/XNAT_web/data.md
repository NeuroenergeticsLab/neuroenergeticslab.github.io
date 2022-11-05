---
layout: default
title: Upload data in Xnat.
parent: XNAT web
grand_parent: Data Pipeline
nav_order: 3
---

## Upload data in XNAT.
- For easier upload you can download ([XNAT Desktop Client](https://wiki.xnat.org/xnat-tools/xnat-desktop-client-dxm)). Install the UI and login with your XNAT web user name and password.

![image](https://user-images.githubusercontent.com/40626584/200124341-90a04c8e-3b7d-4c73-a57f-2754965a34e9.png)

- And then Click on "Upload". Click on the project in which you want to upload the data to. Select the file from your local machine and click on next.

_Note: You can only upload dataset to projects already created on XNAT website_.
![image](https://user-images.githubusercontent.com/40626584/200124496-efdaf98b-dc3e-4db4-a743-7e8584eae9cf.png)

- Choose between in making a `New Subject" or add to and existing Subject. Then click on Next. 

![image](https://user-images.githubusercontent.com/40626584/200124588-ed1c5edd-8460-4a31-b1b1-9bc071f431cb.png)

- Before uploading you can also inspect the images.
![image](https://user-images.githubusercontent.com/40626584/200124656-a287a323-6e45-4e10-95a9-fd70a640a2de.png)

- You can now, find the uploaded scans in your project directory in XNAT. If not, then click on your Project, then click on "View Prearchive". Archive the files to confirm your changes.
![image](https://user-images.githubusercontent.com/40626584/200135333-5b860550-4abb-49c6-8532-896aecd67b1e.png)



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



## Share files within XNAT.
You can also share files within XNAT, without local transfer. Now, to share the files, do the following:
- Open the projrct from where you want to transfer the file.
- Click on the subject whose data you want to transfer.
- Click on the ``Projects`` Tab, choose the project in which you want to share this file.

![image](https://user-images.githubusercontent.com/40626584/200135492-751636c9-2d9b-4a4c-a9ea-37f26bc7c971.png)


_Note: Some analysis does not run when the files are shared between projects._
