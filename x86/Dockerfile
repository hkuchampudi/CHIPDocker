FROM ubuntu:16.04
MAINTAINER Harsha Kuchampudi <harshakuchampudi@gmail.com>
WORKDIR /
RUN apt-get update && apt-get install -y git curl wget usbutils
RUN git clone https://github.com/hkuchampudi/CHIPDocker.git
RUN cd /CHIPDocker && git pull && chmod +x /CHIPDocker/setup_ubuntu.sh
RUN ./CHIPDocker/setup_ubuntu.sh
