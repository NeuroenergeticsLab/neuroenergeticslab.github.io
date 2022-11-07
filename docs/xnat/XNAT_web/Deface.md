---
layout: default
title: Defacing scans
parent: XNAT web
grand_parent: Data Pipeline
nav_order: 5
---

## Defacing Brain Scans.
Since, 2D MR scans can be reconstructed in 3D space. They are a threat to individual patient privacy as, the 3D reconstruction can be used for patient identification.

![image](https://user-images.githubusercontent.com/40626584/200278989-c876e985-0f39-4d26-9c03-f19402c05b9f.png)



Therefore, we use algorithms, to deface the scans like ``pydeface``. 
- Enable ``pydeface`` in the _Project Settings_.
- Then go to the ``Processing Dashboard`` in the ``Actions`` Menu.
- Click on ``MR Sessions``.
- Select the subjects on which you want to run this process. Choose pydeface and launch the process.
![image](https://user-images.githubusercontent.com/40626584/200383199-065f14c9-3059-4a34-9693-b90f07ab14db.png)
- Wait for the process to be completed.

Now, If we look at 3D reconstruction of say T2 weighted scan, it gets defaced like this:


![image](https://user-images.githubusercontent.com/40626584/200383678-01395bd9-c276-4a91-8349-57649767313a.png)


