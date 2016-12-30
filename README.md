# Docker Image for C.H.I.P. SDK

# Table of Contents
1. [Introduction](#introduction)
2. [Installing Docker](#installing-docker)
3. [Creating the CHIP SDK Image](#creating-the-chip-sdk-image)
4. [Flashing the CHIP](#flashing-the-chip)

## Introduction
This repository contains the files necessary to build a C.H.I.P. SDK image to use with [Docker](https://www.docker.com/). If you have never heard of Docker before, you may be wondering what Docker is and why in the world you would want to use it to flash your C.H.I.P. As per the Docker website:
> Docker containers wrap a piece of software in a complete filesystem that contains everything needed to run: code, runtime, system tools, system libraries – anything that can be installed on a server. This guarantees that the software will always run the same, regardless of its environment.

Essentially, this allows us to flash our C.H.I.P. simply and easily regardless of the operating system. Additionally, Docker helps us avoid having to install a bunch of software and messing with our existing OS. Currently, the C.H.I.P documentaion uses Vagrant combined with full virtual machines in order for us to flash the C.H.I.P. Due to the nature of this process, our computer could be slowed-down as well as use a lot of HDD/SSD space :( Docker is a lightweight alternative to all of this!

TL;DR:  Docker provides an easy, lightweight way to install the C.H.I.P. SDK across all operating systems without having to mess with our existing setup!

## Installing Docker
Follow the install guide for your operating system [here](https://www.docker.com/products/overview#/install_the_platform).

## Creating the CHIP SDK Image
1. Once you have installed Docker, clone/download this repository (if you downloaded the .zip file, extract it).
2. Navigate into the CHIPDocker folder.
3. Open a terminal and `cd` into the CHIPDocker folder.
4. Enter the following command to build the image:
> `docker build -t "chip-image" .`
(Don't forget the period at the end; it's important!).
5. Wait for the image to build (it could take a little while). When the image has been successfully been created, you should get the message:
>Successfully built XXXXXXXXXXXX

## Flashing the CHIP
1. Now that we have our Docker image, let's create a container for the C.H.I.P. SDK.
2. Run the following command in the terminal:
>`docker run -it --name chip --privileged -v /dev/bus/usb:/dev/bus/usb -v /dev/ttyACM0:/dev/ttyACM0 chip-image`
3. You should now see a prompt like
>root@XXXXXXXXXXXX:/#
4. At this point, [put your C.H.I.P in FEL mode](http://docs.getchip.com/chip.html#instructions) and plug it into your computer.
5. In the same terminal as before enter the command:
>`cd CHIP-tools`.
6. Now you can run any of the `chip-update-firmware` commands found [here](https://github.com/NextThingCo/CHIP-SDK) to flash your C.H.I.P.
7. If all goes well, the C.H.I.P. should be detected and flashed properly. If the flash succeeded, you should see a message like this on completion:

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
