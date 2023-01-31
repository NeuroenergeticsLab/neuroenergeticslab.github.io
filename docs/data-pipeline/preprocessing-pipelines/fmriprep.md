---
layout: default
title: fMRIPrep
parent: Preprocessing pipelines
grand_parent: Data pipeline
has_children: false
nav_order: 2
---


<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

<br/>	


### 1.0 What is fMRI prep?
fMRIPrep is a functional magnetic resonance imaging (fMRI) data preprocessing pipeline that is designed to provide an easily accessible, state-of-the-art interface that is robust to variations in scan acquisition protocols and that requires minimal user input, while providing easily interpretable and comprehensive error and output reporting. It performs basic processing steps (coregistration, normalization, unwarping, noise component extraction, segmentation, skullstripping etc.) providing outputs that can be easily submitted to a variety of group level analyses, including task-based or resting-state fMRI, graph theory measures, surface or volume-based statistics, etc.

Default steps and the processing flowchart is given below: <sup><sub>(Source: fMRIprep github)</sub></sup>

![image](https://user-images.githubusercontent.com/40626584/215732715-49fd209d-f29d-4b40-b4b1-2644027921f0.png)

### 1.1 Requirements:
-     Unprocessed T1w and BOLD images on XNAT (running MRIQC is fine).

### 1.2 Output:
-     Skull-stripped, intensity corrected, motion corrected, co-registered (BOLD -> T1w) images in native and/or MNI space 
-     If you supplied the fieldmap information (see below), the correction is carried out automatically 
-     BOLD data quality control and confound regressors 
-     Note: No actual regression is carried out automatically 
- An output log file allowing you to review every step fMRIPrep conducted, including visual documentation.

### 1.3 Options for XNAT application
- If you want **fieldmap correction** 
  - Supply fieldmap images from Philips or Siemens 
    - **IMPORTANT:** For Philips data, you have to run the "Fieldmap data prep (philips) for fmriprep" container beforehand.
    - This renames the files and adds metadata to the .json sidecars that enable fmriprep to run the correction 
- If you want **slice-time correction** 
  - Supply slice-timing info in the .json files ("SliceTiming" field) 
  - Usually not recommended for short TRs 
- If you want **freesurfer parcellation** (will take much more time!) 
  - Delete the "fs-no-reconall" text in the container launcher 
- If you (don't) want **ICA** 
  - Leave or delete the "--use-aroma" flag in the container launcher 
- If you want different output spaces and resolutions 
  - Provide the correct space(s) in the launcher.
  - Multiple can be provided, separated by a space (i.e. "anat MNI152NLin2009cAsym" for native + MNI space).
  - Read up on options [here](https://fmriprep.org/en/stable/spaces.html)
 
- For all other options, you have to run fMRIPrep on development with the necessary flags (see next paragraph for some options) 

### 1.4 Additional options via development/docker:
#### 1.4.1 Manual set up
- To run fMRIPrep locally, you need to mount ("-v") your data to this docker container: poldracklab/fmriprep:latest
- You also need to mount a Freesurfer license , which you can obtain [here](https://surfer.nmr.mgh.harvard.edu/fswiki/License).
- All your data needs to be BIDS compliant
  - Structure: .../sub-XXX/anat[...]func[...]fmap
  - .nii.gz and .json files
- Depending on what you need, change the command line arguments [here](https://fmriprep.org/en/stable/usage.html)
  - The "default" command:
    - § fmriprep RAWDATA_PATH OUTPUT_PATH participant --fs-no-reconall -w WORKING_DIR_PATH --mem_mb 24000 --write-graph --dummy-scans 0 --fs-license-file LICENSE_PATH
    - Explanation:
    	- Run fmriprep
    	- Take RAWDATA_PATH a as input (e.g. /RAID1/tmp/mystudy/rawdata)
    	- Take OUTPUT_PATH as output
    	- Analyse participants separately (this argument literally has to say "participants".
    	- Do not run freesurfer for parcellation or surface reconstruction (saves a lot of time)
    	- Save intermediate results to WORKING_DIR_PATH (helps debugging a lot)
    	- Allocate 24gb of memory (higher values might crash it!)
    	- Produce a graph/flowchart of the process
    	- Specify that no dummy scans are in the BOLD file (default for Philips)
    	- Find the Freesurfer license in LICENSE_PATH
![image](https://user-images.githubusercontent.com/40626584/215750149-c89bc312-01a3-440a-88e5-91c142ceccf6.png)

				
