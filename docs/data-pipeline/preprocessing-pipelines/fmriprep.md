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
      - If you supplied the fieldmap information (see below), the correction is carried out automatically 
-     BOLD data quality control and confound regressors 
      - Note: No actual regression is carried out automatically 
- An output log file allowing you to review every step fMRIPrep conducted, including visual documentation 
