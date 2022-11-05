---
layout: default
title: Bids description.
parent: XNAT web
grand_parent: Data Pipeline
nav_order: 4
---

## Add BIDS Description to the series
This step is required to convert the DICOM files you just uploaded in the XNAT website into the BIDS structure. 
The Brain Imaging Data Structure (BIDS) is a standard for organizing, annotating, and describing data collected during neuroimaging experiments. 
It is done so that you do not loose metadata on your file structure. 

Also before running any other analysis, this step is a pre-requisite. 
The purpose of this step is to match series descriptions on XNAT with correct BIDS names.  

### Create a config Folder
- Open your project page. It will look something like this. Here you can see the subjects and the actions menu.
![image](https://user-images.githubusercontent.com/40626584/200135858-5afc97b1-cee7-40b4-ba40-abddde22fad6.png)

- Now, in the actions menu, click on "Manage Files". By default you will see a blank folder structure. 
![image](https://user-images.githubusercontent.com/40626584/200135954-e42d46dd-633f-4436-a69d-00f8327b0d64.png)


- Click on Add Folder. Choose "Resources" as level and name the project "config" (make sure it's not in caps) and then click on create.  

![image](https://user-images.githubusercontent.com/40626584/200136018-163a29ad-4ff1-49f0-844f-87360248b922.png)

  - The folder structure will now look like this: 
  ![image](https://user-images.githubusercontent.com/40626584/200136032-1bcd113d-762d-4da3-8b00-4ded3f6884d1.png)

- Now, click on the individual subjects, which you want to convert into BIDS from DICOM. As an example suppose we look into "Sub_01". Open Sub_01, click on MR sessions (highlighted in the below figure in blue)
![image](https://user-images.githubusercontent.com/40626584/200136090-a754ab05-92a9-4cf6-af21-6131ca19fe90.png)


  - So, the given subject has scans 17, 26, 38, 39 and 40. Now click on Manage Files. 
![image](https://user-images.githubusercontent.com/40626584/200136111-0158e078-3855-4942-9d4e-22e3ed5ec87c.png)
![image](https://user-images.githubusercontent.com/40626584/200136121-54c9996d-9bc1-4b89-9446-41e8ab9943f1.png)


- As you can see apart from Scan 17, other scans only has DICOM files. Now we will convert the DICOM file of scan 26 and 38 into BIDS structure as well. For that copy the series description against the target scans.  
- Now open any editor (Notepad ++, VS Code or any other), create a file with name 'bidsmap.json'. "Follow the given code structure", note that for each scan there is a { } block separated from another { } with comma". It would be good idea to to check if your json file is valid here: https://jsonlint.com/  
**NOTE:** NOTE: BIDSNAME used here are not according to convention, to add valid BIDSNAME follow this guideline. KEEP the same series description. You can look up the correct bids specification here (page 23 for MRI) <"\ValNeuroLab - Documents\DataPipeline\BIDS-Specification-v1.4.0.pdf>(location in ValNeuro One drive)
![image](https://user-images.githubusercontent.com/40626584/200136178-f2aceb96-0688-45e8-89c1-b402af0788ae.png)

- Save the file as bidsmap.json and click on upload File as in here. 
![image](https://user-images.githubusercontent.com/40626584/200136197-a7cd76a3-31d2-4140-99a5-c6d3ec39277f.png)

- Now your file structure will look like this.
![image](https://user-images.githubusercontent.com/40626584/200136226-ef10e75c-35c2-46d8-acd2-1e280e1bebf6.png)

## Run Docker Container.
- Open your project and then go to **Project > Actions > Project settings**.
- Enable ``dcm2bids PAR-REC compatible`` command.
![image](https://user-images.githubusercontent.com/40626584/200136364-d0c3e038-4555-4d87-8224-7e37e0cea094.png)


- Now, Click on "Processing Dashboard" and "MR session" (or whatever session you are working on). Click on the "Sub_01" checkbox. Go to the "Select Job" menu and select "dcmparrec2niftibids". 
- And then click on Launch Job. And then click on "Run Container". 
![image](https://user-images.githubusercontent.com/40626584/200136394-26aa1071-d781-4a1d-849f-6318dc831517.png)

- Wait for Background process to complete till 100%. Now, click on Sub 01, and MR session and then go to Manage Files. As you can see BIDS structure has now formed for scans 26 and 38. 
 ![image](https://user-images.githubusercontent.com/40626584/200136423-335ab4a2-fa09-4ae9-adc9-2c9e90a8eca9.png)





