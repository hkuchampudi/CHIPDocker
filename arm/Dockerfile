FROM armv7/armhf-ubuntu
MAINTAINER Harsha Kuchampudi <harshakuchampudi@gmail.com>
WORKDIR /
RUN apt-get update && apt-get install -y git curl wget usbutils
RUN git clone https://github.com/hkuchampudi/CHIPDocker.git
RUN cd /CHIPDocker && git pull && chmod +x /CHIPDocker/arm/setup_ubuntu_arm.sh
RUN ./CHIPDocker/arm/setup_ubuntu_arm.sh
