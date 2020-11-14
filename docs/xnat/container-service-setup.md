---
layout: default
title: Container service setup
parent: XNAT
nav_order: 4
---

1. Go to [http://localhost](http://localhost) and login
2. Set the Path Translation by clicking on **Administer** (top bar) &#8594; **Plugin Settings**
    > ![step 2](/pics/5.png)

3.  Edit local socket
    > ![step 3](/pics/6.png)

4. Change the Docker Server Path Prefix to the location of the `xnat_data` directory set up in the installation page, step (2a)
    > ![step 4](/pics/7.png)

5. Set the Processing URL (**Administer** &#8594; **Site Administration** &#8594; **Pipeline Settings** &#8594; **Processing URL**) to `http://host.docker.internal` in Mac or to the IP of the host machine in Linux
    > ![step 5](/pics/8.png)

6. Add a docker image (**Administer** &#8594; **Plugin Settings** &#8594; **Image & Commands** &#8594; **Add New Image**), e.g. the `xnat/dcm2bids-session`
    > ![step 6](/pics/9.png)

7. Once the image is pulled, it will appear on the **Image & Commands** tab within the **Plugin Settings** page (6)

8. If the docker image added in (6) is [XNAT Ready](https://wiki.xnat.org/pages/viewpage.action?pageId=38339164), it will have commands already added into the command, e.g. the `xnat/dcm2bids-session image`, otherwise, click on **Add new command** button. A window will appear into which you can paste or type the command JSON ([Container service Commands](https://wiki.xnat.org/display/CS/Command))

