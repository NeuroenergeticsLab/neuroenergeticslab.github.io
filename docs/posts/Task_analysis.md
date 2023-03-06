---
layout: default
title: fMRI Task Analysis
parent: Blog posts
nav_order: 3
---

# Task Analysis 

## Step-by-step instruction 
Enable the following three scripts for your project on xnat:
1. Fieldmap data prep (philips) for fmriprep (vallab/fmapprep:1.2) 
2. fmriprep_v20.2.3 (nipreps/fmriprep:latest) 
3. post-fMRIPrep task analysis (valneurolab/fsltask:1.1)

### 1. Run fieldmap preparation script (optional, only for DICOMs so far) on xnat 

Fieldmap data prep (philips) for fmriprep (vallab/fmapprep:1.2) 
Renames the fmap files and adds to the json files so fieldmap correction can be performed by fMRIPrep 
Needs identifier strings to identify the right fMRI and fieldmap sequences (these have to be unique and match part of the names of your sequences) 

![image](https://user-images.githubusercontent.com/40626584/223187815-a7b0c6d8-7594-48dc-bb03-bf77d5fa89ae.png)

### 2. Run fMRIprep (v20.2.3 is the newest one, on xnat) 

fmriprep_v20.2.3 nipreps/fmriprep:latest 
- Example with both MNI6NLin in 2mm space (compatible with FSL space) and native space (anat = T1w) output, without ICA AROMA run

![image](https://user-images.githubusercontent.com/40626584/223188076-7bc659cd-66a1-498f-b010-efcffcd8305d.png)

Output: resource named fmriprepv20.2.3 with preprocessed, fieldmap corrected files in all spaces defined, confound variables, QC, …. 

### 3. On Jupyterhub: Run task-analysis preparation script 
- We have to   
  a. Add a sub-XXX_events.tsv file (with condition onsets, time etc. in seconds) for every subject 
    i. WARNING: This file has to have the same BIDS fields as your bold file. Important are: 
      1. The default ones that most BOLD files have: Sub- and task- 
      2. For PET: acq- 
      3. When in doubt, give your events file all the BIDS fields your BOLD file has 
  b. Change the dataset_description.json file which was the output of fMRIprep v20.2.3 
- For example script see: **neuroenergeticslab_notebooks/erc-wp1/B_Postfmriprep_prepare_task_analysis **

![image](https://user-images.githubusercontent.com/40626584/223189004-ea4b1ce6-dc4f-4295-aac7-cb9cb0c9e902.png)

- The events.tsv file has to be stored for each subject under a new **'events' - resource!**

![image](https://user-images.githubusercontent.com/40626584/223189156-42301ea2-c781-4723-8eb9-8e94e997a686.png)

- Example for events.tsv file

![image](https://user-images.githubusercontent.com/40626584/223189270-86de37fd-0366-4347-87e3-b4784130e543.png)


### 4. Run Task analysis script (on xnat) 

post-fMRIPrep task analysis (valneurolab/fsltask:1.1) 

Enable the script for your whole project and set up your project-specific specifications ('Set Defaults') 
Example:

![image](https://user-images.githubusercontent.com/40626584/223189408-8a416a5c-9c06-45ae-b449-e6c188e631f5.png)


--> **conditions** have to match condition names in events.tsv file 

--> for each **contrast**, you have to define the conditions (separated by comma), the weights (not separated) and the testtype (T-test in this case), contrasts are separated by white spaces 

--> the **confound**s have to be listed as in the output of the fmriprep, separated by white space (e.g.: csf white_matter dvars framewise_displacement trans_x trans_y trans_z rot_x rot_y rot_z a_comp_cor_01 a_comp_cor_02 a_comp_cor_03) 

--> define in which **space** you want to run the analysis (native space = T1w or e.g. MNI152NLin6Asym) 

--> **hpf** = high pass filter to be applied( in seconds) 

--> you have to give a valid identifier for the fMRI **task** run

- Finally: Run the task analysis for every subject! 

![image](https://user-images.githubusercontent.com/40626584/223189753-ca950c49-e0e7-498d-87ac-8f20e3dec456.png)

### FAQs:
- **Confound input**: The confounds must be entered with their full name (based on the fmriprep output), each separated by a whitespace 
Example:  
  - csf white_matter dvars framewise_displacement trans_x trans_y trans_z rot_x rot_y rot_z a_comp_cor_01 a_comp_cor_02 ... 
- **fMRIPrep version/ adapt dataset_decription file**: The BIDS standard changes and new fmriprep Version adapt their output slightly. To work with the task analysis, the dataset_description.json inside the fmriprep resource must be changed from 
'''
  
  "GeneratedBy": [ 
  { 

  "Name": "fMRIPrep", 

  "Version": "20.2.4", 

  "CodeURL": "https://github.com/nipreps/fmriprep/archive/20.2.4.tar.gz" 

  } 

  ], 

 

  To 

 

  "PipelineDescription": 

  { 

  "Name": "fMRIPrep", 

  "Version": "20.2.4", 

  "CodeURL": "https://github.com/nipreps/fmriprep/archive/20.2.4.tar.gz" 

  }, 
 '''
