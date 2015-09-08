---
layout: post
title: Docker Toolbox - Docker on Windows made dead simple (installation tutorial)
---
####Introduction
There are two types of Docker containers, one type running on a Linux API and one on a Windows Server API. Most of the Docker images on the docker hub today, if not all, are Linux containers and need a Linux OS to run. This is a problem if you are running Windows as your default OS and is where the Docker Toolbox enters the scene. It offers a package installer including 

>**The Virtual Box.**
>	This is the hypervisor that makes it possible to run a Linux OS image inside Windows. Your docker containers will run inside of the Linux OS.

>**Docker Machine for Windows.**
>	Helps with creation and configuration of a Docker host inside of the VirtualBox.
	
>**Docker Client for Windows.**
>	The heart of the Docker infrastructure is the Docker host. That is where all the containers run. To send commands like spawn up a new container, or tear down a used one, you also need a Docker client. One Linux client is included in the Docker image, but this is the Windows client. These Docker clients are mainly a wrapper around the Docker REST API.
	
>**Kitematic for Windows.**
>	A GUI Docker client. Simplifies container overview and management compared to the command line clients.
	
>**Git for Windows.**
>	A basic git client.
	
####Installation
- Go to [the docker toolbox site](https://www.docker.com/toolbox) and download the latest version of the windows installer. This blogtutorial is based on Docker Toolbox version 1.8.1c and was done on Windows 10 Pro. 
- Run the installer to install all its components. Two shortcuts are created on the start menu, the Docker Quickstart Terminal and the Kitematic. 
- Begin with the Docker Quickstart terminal. The first time you run this it will take a minute to start the Virtual Box, install and configre the Docker host. Pay attention to the IP address shown at the end of the docker startup. This is the address to use when reaching a container from the Windows world.
- Now go back to the shortcuts and start Kitematic. You need a Docker Hub account to sign in, but it is free and simple to register.

####Hello World from inside docker
Once everything is setup it is time for a classical Hello World. In Kitematic click the +New button in the container frame and choose to create the kitematic Hello World nginx image. Kitematic now sends a command to the Docker host to download the image from the Docker Hub and spin it up. 

Nginx is a simple HTTP server that  now start inside of container and listens to port 80. Under the Kitematic settings/port tab you can find the ip address together with the port that docker mapped this containers port 80 to. Clicking on the link will bring up a browser that renders the Hello World web page.

As a last step we will now mount a folder in the container onto a folder in Windows. This is done in Kitematic on the Settings/Volumes tab. The containerfolder to map is already selected. Click change and select a destinaion folder. Open the folder in file explorer and you should find the index.html file from the container. Edit the file, save changes and update your browser. Your changes should be directly visible on the Hello World webpage.
