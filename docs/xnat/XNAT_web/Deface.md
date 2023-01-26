---
layout: default
title: Defacing scans
grand_parent: Data Pipeline
nav_order: 7
---

parent: XNAT web manual
## Defacing Brain Scans.
With improvements in facial recognition softwares and high scan quality, there is an increased risk of participants being identified, as 2D MR scans can be reconstructed in 3D space. They are a threat to individual patient privacy, even when all other personal information has been removed.

Therefore, we use algorithms, to deface the scans like ``pydeface``. 
- Enable ``pydeface`` in the _Project Settings_.
- Then go to the ``Processing Dashboard`` in the ``Actions`` Menu.
- Click on ``MR Sessions``.
- Select the subjects on which you want to run this process. Choose pydeface and launch the process.
![image](https://user-images.githubusercontent.com/40626584/200383199-065f14c9-3059-4a34-9693-b90f07ab14db.png)
- Wait for the process to be completed.

- After removing the facial features the scan will look like this:

![image](https://user-images.githubusercontent.com/40626584/214870007-1e4a4ac7-b92b-45a7-98c8-4757a5063bd6.png)


- Now, If we look at 3D reconstruction of say T2 weighted scan, it gets defaced like this:

![image](https://user-images.githubusercontent.com/40626584/200383678-01395bd9-c276-4a91-8349-57649767313a.png)


