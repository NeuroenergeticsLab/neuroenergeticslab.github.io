---
layout: default
title: Run docker container
parent: XNAT web manual
grand_parent: Data pipeline
nav_order: 7
---

## How to Run Docker container on your data

1. Before running containers that require BIDS data structure, you need to structure your project in a BIDS compliant form. Click [here](./bids-configuration.md) to first do that.
2. Now, Go to the home page of your project and in the Actions menu click on "Project Setting".

![image](https://user-images.githubusercontent.com/40626584/214611509-33cb2f16-4aa8-41c4-a27f-20388ed59642.png)

3. Here you will see a list of containers like this. Turn them on to use it. For example in this case, MRIQC is enabled already.
![image](https://user-images.githubusercontent.com/40626584/214611848-c7bb5ebe-a04e-4336-83dd-2e570491efde.png)

4. Now to use the containers, go to the Actions menu in the "Processing Dashboard". You can see the name of the containers (here MRIQC) in the drop down menu. Click on your project and select "Lauch Job" to get the process done.
![image](https://user-images.githubusercontent.com/40626584/214612805-c278f4dd-19d3-42ed-a9b3-2701a5768d65.png)
