# this docker file is used to build the docker image for picsimlab

# base image
FROM ubuntu:20.04

# metadata
LABEL base.image="ubuntu:20.04"
LABEL version="1"
LABEL software="Picsimlab"
LABEL software.version="0.8.12"
LABEL description="Picsimlab is a simulator for educational propuses, it simulates a microcontroller board with peripherals like LCD, ADC, EEPROM, etc. It can be used to learn how to program microcontrollers or to develop applications without the need of buying the real hardware."
LABEL website="github.com/lcgamboa/picsimlab"
LABEL license="github.com/lcgamboa/picsimlab"
LABEL maintainer="Mohamed Aly Amin"

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

# install picsimlab

RUN wget