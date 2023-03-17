# MPLAB X IDE Docker Container

This repository contains a Dockerfile to create a Docker container with MPLAB X IDE v5.45 and XC8 Compiler v2.30 installed.

## Prerequisites

1. Install Docker on your system. Follow the [official installation guide](https://docs.docker.com/engine/install/) for your operating system.

2. Install the `x11-xserver-utils` package on your host machine (for Linux users) to allow the Docker container to use the host's X server:

## Building the Docker Image

1. Clone this repository and navigate to the directory containing the Dockerfile.

``` sudo apt-get install x11-xserver-utils ```
2. Build the Docker image:

```docker build -t mplabx-ide .```

## Running the Docker Container

1. Allow connections to your X server from local Docker containers:

``` xhost +local:docker ```
2. Run the Docker container and share the necessary resources for the graphical interface to work:

``` docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix mplabx-ide ```

This command will start a new Docker container, and the MPLAB X IDE should launch with a graphical interface.

**Note:** Allowing connections to your X server may have security implications. Read about X server security before applying these changes.
