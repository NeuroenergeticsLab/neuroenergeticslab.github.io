---
layout: default
title: Create Docker images
nav_order: 1
parent: Tutorials
---

## Intro

Docker images are templates for Docker containers. You can create your own image or use an already existing one and build on top of it. To build a docker image, you should write a Dockerfile - a text file with instructions on how to create the image. Once the image is built, a container launched from that image can run commands. The advantage is that containers are self-conained and isolated enviroments - they can be shared and will work everywhere exactly the same.

In this tutorial, I will create a simple Docker image to highlight the main points. The idea is to make a container that will send a request to a weather forecast service and print out the contents to the terminal.

## Create a Dockerfile 

1. First, I create a directory for my image and add a README file.  
`mkdir weather-forecast && cd weather-forecast`  
`echo "This is a container that prints out a current forecast" > README`

1. I then open a Dockerfile and start writing the instructions.  
`nano Dockerfile`

## Write commands that create the image

1. In the beginning of the Dockerfile, I'm selecting a base image on top of which I want to build my image. In this example, I use an empty Ubuntu image, but one can use any image avilable on Docker Hub or installed locally.  
`FROM ubuntu:20.04`

1. Below, I'm updating the Ubuntu repositories and installing the `curl` command.  
`RUN apt-get update -y && apt-get install -y curl`  
> Note that every `RUN` command creates a new [layer](https://docs.docker.com/storage/storagedriver/#images-and-layers) in a container. It is better to use as little of them as possible. So if you need to install multiple packages, include them all in one line.

1. By default, Docker runs images as root. If that is not possible, create a new user and change to that user. `useradd` command below creates a new user account. `-ms /bin/bash` creates a home directory for that user and uses `bash` as a default shell. `sunny` is the user name of the new account. The `"sunny:password"` forwarded to `chpasswd` command changes the password. This is not strictly necessary, but sometimes can be useful.  
`RUN useradd -ms /bin/bash sunny && echo "sunny:password" | chpasswd`

1. Set default working directory inside the container. This directory exists because I created it with the `-m` switch above.  
`WORKDIR /home/sunny`

1. Change the user. All commands below this line will execute from that user's account. Can be handy when setting up environment variables.  
`USER sunny`

1. Let's say I want to specify my city and the timezone in the container's environment. I can access them with `$TZ` or `$CITY`.  
`ENV TZ Europe/Berlin`  
`ENV CITY Munich`

1. Now I copy the README file I created in the beginning so it's also available inside the container once it's launched. This command will copy the README file from my current working directory to the current working directory inside the container (the one I specified with the `WORKDIR` command). This is useful when you need to include a script or other important files inside a container.  
`COPY ./README .`

1. Finally, I set a default command for my image. This command will run when I launch a container. I can overwrite this behaviour later and use another command if I need. I'm using [wttr.in](https://wttr.in/) service here (which is, by the way, the coolest way to check the weather! ⛈). Because I already set my city before in the `$CITY` environment variable, I can use it here. I will copy the output to a text file with the `tee` command so I can access it later. See the [reference](https://docs.docker.com/engine/reference/builder/#cmd) for details on how to format this.  
`CMD [ "/bin/bash", "-c", "curl --silent wttr.in/$CITY | tee /home/sunny/current-weather.txt" ]`

1. Now the Dockerfile is ready! The final file looks like this:  

```
FROM ubuntu:20.04
RUN apt-get update -y && apt-get install -y curl
RUN useradd -ms /bin/bash sunny && echo "sunny:password" | chpasswd
WORKDIR /home/sunny
USER sunny
ENV TZ Europe/Berlin
ENV CITY Munich
COPY ./README .
CMD [ "/bin/bash", "-c", "curl --silent wttr.in/$CITY | tee /home/sunny/current-weather.txt" ]
```

## Build the image

1. This step will create the image. The `-t` argument assigns a name and a version to the image. Specifying the version for the image is possible after the colon. The dot at the end of the line is easy to miss but is important - it says that the Dockerfile is located in the current directory.  
`docker build -t valneurolab/weather-report:latest .`

1. See if that worked - the image should appear in the list.  
`docker images | grep weather`


## Launch the container

- Now, I need to use the `docker run` command and provide the name of my image. The `--rm` argument makes sure that the container is removed after it has executed its commands. (Otherwise, the container will persist and will be visible with `docker ps -a` as exited).  
Let's hope for the best!  
`docker run --rm valneurolab/weather-report:latest`

![output-screenshot](https://user-images.githubusercontent.com/25939378/215902889-86930e58-bdca-4bba-b009-8a5389280fec.png)
A bit involved, but cool way to check the weather 🙂

-  The container accesses wttr.in and prints the results to the stdout - just what I wanted! Since I specified the default command in the `CMD` line, I don't need to type the command again. However, if I wanted to know the weather in Berlin, I could specify that in a custom command that will override the one I specified in the Dockerfile.  
`docker run --rm valneurolab/weather-report:latest curl --silent wttr.in/Berlin`

- Or, I can overwrite the `$CITY` variable I set in the Dockerfile withe the `-e` argument:  
`docker run --rm -e "CITY=Berlin" valneurolab/weather-report:latest`  

-  It is also possible to run a different command altogether. For example, if I just wanted to list the contents of the home directory inside the contianer:  
`docker run --rm valneurolab/weather-report:latest ls -lh /home/sunny`

-  If you're curious about the contents of the container, you can execute the following command to log into the container. The `-it` argument tells Docker to run this in the interactive mode so we can enter commands and get outputs.  
`docker run --rm -it valneurolab/weather-report:latest bash`


-  Finally, I would like to access the text output that my command creates (the `tee` command in the `CMD` line redirects the output to both stdout and a file). To do that, I need to **mount** a directory on my computer to somewhere inside the container. That is possible with the `-v` argument.  
I specify the path in my local computer first and the path inside the container after the colon: `</local/path>:</container/path>`. I also need to give write permissions to my working directory so the container can save the output there: `cd .. && chmod -R 777 weather-report` (we run the container from non-root user sunny). After executing this command, the `current-weather.txt` file with the container's outputs should appear in my weather-report directory.   
`docker run --rm -v /home/tumnic/rbelenya/weather-report:/home/sunny valneurolab/weather-report:latest`

## Save/load the image

If I need to send my image to someone, I can save the image to an archive:  
`docker save valneurolab/weather-report:latest -o weather-report-image.tar.gz`

And my recipient can load it with:  
`docker load -i weather-report-image.tar.gz`

--- 
References:

[1](https://docs.docker.com/engine/reference/builder/) Description of Dockerfile commands  
[2](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) Dockerfile best practices  
[3](https://docs.docker.com/engine/reference/run/) Docker run reference - useful to launch containers
