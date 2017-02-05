# Dockerfile for CHIP SDK

## Table of Contents
- [Introduction](#introduction)
- [Installing Docker](#installing-docker)
- [Installing Docker on the CHIP](#installing-docker-on-the-chip)
- [Creating the CHIP SDK Image](#creating-the-chip-sdk-image)
    - [For Docker on x86 Systems](#for-docker-on-x86-systems)
    - [For Docker on the CHIP](#for-docker-on-the-chip)
- [Flashing the CHIP](#flashing-the-chip)
- [Resources](#resources)

## Introduction
This repository contains the Dockerfiles and setup scripts necessary to build Docker images containing the CHIP SDK for Docker running on x86 systems as well as the CHIP. If you are new to Docker, you may be wondering what Docker is and why you would want to use it to flash your CHIP. From Docker's website:
> Docker containers wrap a piece of software in a complete filesystem that contains everything needed to run: code, runtime, system tools, system libraries – anything that can be installed on a server. This guarantees that the software will always run the same, regardless of its environment.

Essentially, Docker allows us to flash the CHIP easily regardless of the host operating system. Additionally, Docker helps us avoid having to directly install new packages and software on our host system, and instead offers minimal virtual machines (called containers) which we can install the software onto and delete once we are done with them. Currently, the CHIP documentation uses Vagrant combined with full virtual machines to flash the CHIP. This process uses more overhead and therefore could slow down our system as well as use more HDD/SSD space :( Docker is a lightweight, cross platform solution to this!

## Installing Docker
Follow the install guide for your operating system [here](https://www.docker.com/products/overview#/install_the_platform).

## Installing Docker on the CHIP
While it is still experimental, you can install Docker on your CHIP by SSHing into the CHIP and issuing the command `curl -sSL https://github.com/DieterReuter/arm-docker-fixes/raw/master/002-fix-install-docker-on-chip-computer/apply-fix-002.sh | bash`. You can follow [the guide here](http://blog.hypriot.com/post/install-docker-on-chip-computer/) for more detailed instructions.

## Creating the CHIP SDK Image

### For Docker on x86 Systems
1. Once you have downloaded Docker, clone/download this repository (if you downloaded the .zip file, extract it).
2. Open a terminal and `cd` into the CHIPDocker folder.
3. Next, `cd` into the `x86` folder.
4. Enter the following command to build the image: `docker build -t "chip-image" .` (be sure that you add the period at the end; it's important).
5. Wait for the image to build (it could take a while).
6. When the image has been successfully built, you should get the message: `Successfully built XXXXXXXXXXXX`.

### For Docker on the CHIP
1. Once you have downloaded Docker, clone/download this repository (if you downloaded the .zip file, extract it).
2. Open a terminal and `cd` into the CHIPDocker folder.
3. Next, `cd` into the `arm` folder.
4. Enter the following command to build the image: `docker build -t "chip-image" .` (be sure that you add the period at the end; it's important).
5. Wait for the image to build (it could take a while).
6. When the image has been successfully built, you should get the message: `Successfully built XXXXXXXXXXXX`.

## Flashing the CHIP
1. [Put your C.H.I.P in FEL mode](http://docs.getchip.com/chip.html#instructions) and plug it into your computer.
2. Now that we have our Docker image, let's create a container for the CHIP SDK. Run the following command in the terminal: `docker run -it --name chip --privileged -v /dev/bus/usb:/dev/bus/usb chip-image`.
3. You should now be in the Docker container shell, you should see a prompt like: `root@XXXXXXXXXXXX:/#`.
4. Now enter the command: `cd CHIP-tools` into the Docker shell.
5. Now you can run any of the `chip-update-firmware` commands found [here](https://github.com/NextThingCo/CHIP-SDK) to flash your C.H.I.P.
6. If all goes well, the C.H.I.P. should be detected and flashed properly. If the flash succeeded, you should see a message like this on completion:

```
FLASH VERIFICATION COMPLETE.


   #  #  #
  #########
###       ###
  # {#}   #
###  '%######
  #       #
###       ###
  ########
   #  #  #



CHIP is ready to roll!
```

## Resources
- [C.H.I.P. User Documentation](http://docs.getchip.com/chip.html)
- [C.H.I.P. SDK Repository](https://github.com/NextThingCo/CHIP-SDK#help-section)
- [Docker Documentation](https://docs.docker.com/)
