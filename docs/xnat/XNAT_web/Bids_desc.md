---
layout: default
title: Bids description.
parent: XNAT web manual
grand_parent: Data Pipeline
nav_order: 6
---
<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>


## 1.0 Add BIDS Description to the series
This step is required to convert the DICOM files you just uploaded in the XNAT website into the BIDS structure. 
The Brain Imaging Data Structure (BIDS) is a standard for organizing, annotating, and describing data collected during neuroimaging experiments. 
It is done so that you do not loose metadata on your file structure. 

Also before running any other analysis, this step is a pre-requisite. 
The purpose of this step is to match series descriptions on XNAT with correct BIDS names.  

### 1.1 Create a config Folder
Open your project page. It will look something like this. Here you can see the subjects and the actions menu.
![image](https://user-images.githubusercontent.com/40626584/200135858-5afc97b1-cee7-40b4-ba40-abddde22fad6.png)

Now, in the actions menu, click on "Manage Files". By default you will see a blank folder structure. 
![image](https://user-images.githubusercontent.com/40626584/200135954-e42d46dd-633f-4436-a69d-00f8327b0d64.png)


Click on Add Folder. Choose "Resources" as level and name the project "config" (make sure it's not in caps) and then click on create.  

![image](https://user-images.githubusercontent.com/40626584/200136018-163a29ad-4ff1-49f0-844f-87360248b922.png)

The folder structure will now look like this: 
![image](https://user-images.githubusercontent.com/40626584/200136485-4d62b06f-cd28-42cb-985d-cb91eb58c7b0.png)

### 1.2 Check the names of your experiments scans.

Now, click on the individual subjects, which you want to convert into BIDS from DICOM. As an example suppose we look into "Sub_01". Open Sub_01, click on MR sessions (highlighted in the below figure in blue)
![image](https://user-images.githubusercontent.com/40626584/200136090-a754ab05-92a9-4cf6-af21-6131ca19fe90.png)


So, the given subject has scans 26, 38, 39 and 40. Now click on Manage Files. 
![image](https://user-images.githubusercontent.com/40626584/214589657-280880f7-f69c-4dbf-8a38-71f0a89a8ef1.png)
![image](https://user-images.githubusercontent.com/40626584/214584242-53647dc0-62e5-4547-aa0d-5f59d78da08f.png)



As you can see that currently, these scans only has DICOM files. Now we will convert the DICOM files of scan 26 and 38 into BIDS structure . For that *copy the series description against the target scans*.

### 1.3 Create a bidsmap file: 
Now open any editor (Notepad ++, VS Code or any other), create a file with name 'bidsmap.json'.

"Follow the given code structure", note that for each scan there is a { } block separated from another { } with comma". It would be good idea to to check if your json file is valid here: https://jsonlint.com/ . And copy the same description as stated in the above point.

**NOTE:**: Please only use BIDS name according to convention, to add valid BIDSNAME follow this guideline. You can look up the correct bids specification here (page 23 for MRI) <"\ValNeuroLab - Documents\DataPipeline\BIDS-Specification-v1.4.0.pdf>(location in ValNeuro One drive)

![image](https://user-images.githubusercontent.com/40626584/214589024-2f1e1286-50de-4ec6-a07d-7b4513b7808e.png)

Save the file as bidsmap.json.

### 1.4 Upload the bidsmap.json file:
- Click on upload File as in here. 
![image](https://user-images.githubusercontent.com/40626584/200136197-a7cd76a3-31d2-4140-99a5-c6d3ec39277f.png)

- Now your file structure will look like this.
![image](https://user-images.githubusercontent.com/40626584/200136226-ef10e75c-35c2-46d8-acd2-1e280e1bebf6.png)

## 1.5 Activate Dicom to BIDS container.
- Open your project and then go to **Project > Actions > Project settings**.
- Enable ``dcm2bids PAR-REC compatible`` command.
![image](https://user-images.githubusercontent.com/40626584/214590327-64ed85fa-cb87-4408-a8fb-e417f3af6df4.png)

NOTE:*Please make sure that you activate the 2021 version*

### 1.6 Run the Container:
- Now, Click on "Processing Dashboard" and "MR session" (or whatever session you are working on). Click on the "Sub_01" checkbox. Go to the "Select Job" menu and select "dcmparrec2niftibids". 
- And then click on Launch Job. And then click on "Run Container". 
![image](https://user-images.githubusercontent.com/40626584/200136394-26aa1071-d781-4a1d-849f-6318dc831517.png)

- Wait for Background process to complete till 100%. 
 
### 1.7 Check the Results: 
Now, click on Sub 01, and MR session and then go to Manage Files. As you can see BIDS structure has now formed for scans 26 and 38. 
 ![image](https://user-images.githubusercontent.com/40626584/214585147-9b0b4da6-5986-4842-8f5d-c3d3d13f8ab9.png)






