---
layout: default
title: Create Pseudo CT Images
parent: Cheatsheet
grand_parent: Data Pipeline
nav_order: 1
---


# 1.0 Create pseudo CT images


1. Download the NIFTI images for your T1 sequence
	- Go to *Project > Actions > Download images*
	- Select sessions, scan data type (NIFTI), scan type [(Fig.1)](#Cheatsheet/CT/Download)


	<a name="Cheatsheet/CT/Download"></a>

	| ![Download NIFTI images](../../../pics/CT_download.png) | 
	|:--:| 
	| **Fig.1** *Download NIFTI images.* |


	- Unzip the archive. To extract the compressed NIFTI files from the directory structure, run command from the data folder:
	`cp ./*/*/NIFTI/*.gz ./`

<br/>


2. Upload the NIFTI files to CT synthesis tool [(Fig.2)](#Cheatsheet/CT/Synthesis)
	- Go to http://niftyweb.cs.ucl.ac.uk/program.php?p=PCT
	- Enter email, select Input Image Modality T1-weighted MRI, Parameters Optimise for accuracy
	- Select 5 files at a time
	- It takes about an hour for one file to process


	<a name="Cheatsheet/CT/Synthesis"></a>

	| ![Online CT synthesis tool](../../../pics/Synthesis_tool.png) | 
	|:--:| 
	| **Fig.2** *Online CT synthesis tool.* |

<br/>





