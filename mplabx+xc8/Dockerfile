# this file is used to build the docker image for mplab x ide v5.45 on ubuntu 20.04 LTS
# this file is based on the work of mohamed aly amin 

# base image
FROM ubuntu:20.04

# metadata
LABEL base.image="ubuntu:20.04"
LABEL version="1"
LABEL software="MPLAB X IDE"
LABEL software.version="5.45"
LABEL description="MPLAB X IDE is an integrated development environment (IDE) that supports a wide range of Microchip microcontrollers and digital signal controllers. It runs on Windows, Linux, and macOS operating systems."
LABEL website="https://www.microchip.com/mplab/mplab-x-ide"
LABEL license="https://www.microchip.com/mplab/mplab-x-ide"
LABEL maintainer="Mohamed Aly Amin"
LABEL maintainer.email="contact@mohamedalyamin.com"

USER root
RUN useradd -ms /bin/bash mplab
# install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    libcanberra-gtk-module \
    libcanberra-gtk3-module \
    libgtk-3-0 \
    libxext6 \
    libxrender1 \
    libxtst6 \
    wget \
    xterm \
    sudo \
    libx11-6 libxi6 libfreetype6 libfontconfig1 ca-certificates
# install mplab x ide
RUN wget https://ww1.microchip.com/downloads/en/DeviceDoc/MPLABX-v5.45-linux-installer.tar -O /tmp/MPLABX-v5.45-linux-installer.tar && \
    tar -xvf /tmp/MPLABX-v5.45-linux-installer.tar -C /tmp

# set user to root
RUN  chmod u+x /tmp/MPLABX-v5.45-linux-installer.sh && \
     sudo /tmp/MPLABX-v5.45-linux-installer.sh --nox11 -- --mode unattended --unattendedmodeui none \
     --debuglevel 2 --installdir /opt/microchip/mplabx/v5.45 --8bitmcu 0 --16bitmcu 1 --32bitmcu 0 --othermcu 0  --collectInfo 0 && \
     rm -rf /tmp/MPLABX-v5.45-linux-installer.tar /tmp/MPLABX-v5.45-linux-installer.sh /tmp/MPLABX-v5.45 /tmp/.installer

# install xc8 compiler v2.30
RUN wget https://ww1.microchip.com/downloads/en/DeviceDoc/xc8-v2.30-full-install-linux-x64-installer.run -O /tmp/xc8-v2.30-full-install-linux-installer.run --no-check-certificate && \
    chmod u+x /tmp/xc8-v2.30-full-install-linux-installer.run && \
    sudo /tmp/xc8-v2.30-full-install-linux-installer.run --mode unattended --unattendedmodeui none --debuglevel 4 --prefix /opt/microchip/xc8/v2.30/ --addtopath 1 --netservername 0 --LicenseType FreeMode && \
    rm -rf /tmp/xc8-v2.30-full-install-linux-installer.run

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Add this line before the ENTRYPOINT in your Dockerfile
COPY launch_mplab.sh /usr/local/bin/

# Make the script executable
RUN chmod +x /usr/local/bin/launch_mplab.sh

# Add a user

# Switch to the new user
USER mplab

# Set the working directory

WORKDIR /home/mplab

# Update the ENTRYPOINT to use the script
ENTRYPOINT ["/usr/local/bin/launch_mplab.sh"]
