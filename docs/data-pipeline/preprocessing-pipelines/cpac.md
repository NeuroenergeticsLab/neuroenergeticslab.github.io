---
layout: default
title: C-PAC
parent: Preprocessing pipelines
grand_parent: Data pipeline
has_children: false
nav_order: 1
---

From the [online documentation](https://fcp-indi.github.io/docs/latest/user/index):
> The Configurable Pipeline for the Analysis of Connectomes (C-PAC) is a configurable, open-source, Nipype-based, automated processing pipeline for resting state functional MRI (R-fMRI) data, for use by both novice and expert users. C-PAC was designed to bring the power, flexibility and elegance of the Nipype platform to users in a plug and play fashion—without requiring the ability to program. Using an easy to read, text-editable configuration file or a graphical user interface, C-PAC users can rapidly orchestrate automated R-fMRI processing procedures.

# Configure C-PAC on XNAT

Current verion of C-PAC is 1.4.0 (to be updated soon)

## Enable C-PAC

Go to project > **Project Settings** > **Configure Commands** > click the **Enabled** switch

## Setup the directories

Go back to the project main page -> **Actions** -> **Manage Files** > **Add Folder**

- Select Level: `resources`
- Type in the folder name: `config`


Create two more (empty) directories this way: `data` and `scripts`. These three directories will be mounted to /input/data inside the container.

In the end, the File Manager should look like this:


## Create the pipeline configuration file

You can either dowlnoad a [pre-configured default pipeline](https://fcp-indi.github.io/docs/latest/user/pipelines/preconfig), create a custom pipeline using a [very nice online editor](https://fcp-indi.github.io/C-PAC_GUI/#/), or copy the pipline file from existing project on XNAT.

This file contains configuration for all prepocessing that c-pac will run (e.g. nuisance regression, skull stripping etc).  C-pac website  has [great documentation](https://fcp-indi.github.io/docs/latest/user/preprocessing) about the preprocessing pipelines. One can look up the parameters and accepted values there.


## Upload necessary files to project resources

If the pipeline configuration requires an external file, you need to upload it to `data` folder under the project resources. For example, if you specify the the ROI timeseries should be calculated according to the Schaefer (2018), you have to upload the parcellation file. You can reference this file in the pipeline configuration as `/input/data/Schaefer2018_7nets_400rois.nii.gz` (change the file name).

Go to project > **Actions** > **Manage files** > Select Level: resources, Folder: data > **Choose a file** > **Upload**


## See if that worked

Go to a **Session** -> **Run containers** -> c-pac