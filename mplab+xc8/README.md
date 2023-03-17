# MPLAB X IDE Docker Container

This repository contains a Dockerfile to create a Docker container with MPLAB X IDE v5.45 and XC8 Compiler v2.30 installed.

## Prerequisites

1. Install Docker on your system. Follow the [official installation guide](https://docs.docker.com/engine/install/) for your operating system.

### Linux

2. Install the `x11-xserver-utils` package on your host machine:

```bash
sudo apt-get install x11-xserver-utils
```

### Windows

1. Install [VcXsrv Windows X Server](https://sourceforge.net/projects/vcxsrv/) or another X server application for Windows.

2. Launch VcXsrv with the "Multiple Windows" display setting.

#### Getting the DISPLAY variable

1. Open a Command Prompt or PowerShell window.

2. Determine your computer's IP address. In the Command Prompt or PowerShell window, type the following command:

```powershell
ipconfig
```

3. Look for the "IPv4 Address" field under your active network adapter. Note the IP address (e.g., `192.168.1.100`).

4. Set your DISPLAY variable by combining your IP address with `:0.0`. For example:

```bash
set DISPLAY= 192.168.1.100:0.0
```

Use this value for `<your_display_variable>` when running the Docker container.

### macOS

1. Install [XQuartz](https://www.xquartz.org/) or another X server application for macOS.

#### Getting the DISPLAY variable

1. Launch XQuartz.

2. Open a Terminal window.

3. Run the following command to get your DISPLAY variable:

```bash
echo $DISPLAY
```

This command will output your DISPLAY variable (e.g., `/private/tmp/com.apple.launchd.12345/org.macosforge.xquartz:0`).

Use this value for `<your_display_variable>` when running the Docker container.


## Building the Docker Image

1. Clone this repository and navigate to the directory containing the Dockerfile.

2. Build the Docker image:

```bash
docker build -t mplabx-ide .
```

## Running the Docker Container

### Linux

1. Allow connections to your X server from local Docker containers:

```bash
xhost +local:docker 
```

2. Run the Docker container and share the necessary resources for the graphical interface to work:

```bash
docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix mplabx-ide
```

### Windows

1. Run the Docker container and share the necessary resources for the graphical interface to work. Replace `<your_display_variable>` with the DISPLAY variable noted earlier:

```bash
docker run -it --rm -e DISPLAY=<your_display_variable> mplabx-ide
```

### macOS

1. Allow connections to your X server from the Docker container. Replace `<your_display_variable>` with the DISPLAY variable noted earlier:

```bash
xhost +$(hostname)
```

2. Run the Docker container and share the necessary resources for the graphical interface to work. Replace `<your_display_variable>` with the DISPLAY variable noted earlier:

```bash
docker run -it --rm -e DISPLAY=<your_display_variable> -v /tmp/.X11-unix:/tmp/.X11-unix mplabx-ide
```

This command will start a new Docker container, and the MPLAB X IDE should launch with a graphical interface.

**Note:** Allowing connections to your X server may have security implications. Read about X server security before applying these changes.

