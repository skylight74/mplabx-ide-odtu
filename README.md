# MPLAB and PICSimLab with Docker

This repository contains Dockerfiles for MPLAB X IDE and PICSimLab. It uses tty0tty to connect the two applications via virtual serial ports.

## Prerequisites

1. Install Docker on your machine: https://docs.docker.com/engine/install/
2. Install Docker Compose: https://docs.docker.com/compose/install/

## Installation

### tty0tty

Before running MPLAB X IDE and PICSimLab containers, you need to install tty0tty on your host machine to enable serial communication between the two containers.

1. Clone the tty0tty repository:

```git clone https://github.com/freemed/tty0tty.git```

2. Follow the installation instructions for your specific OS in the `tty0tty/README.md` file.

3. Add your user to the dialout group:

```sudo usermod -a -G dialout $USER```


Log out and log back in for the changes to take effect.

### Building and Running Containers

1. Clone this repository:

```git clone <https://github.com/mohamed9974/mplabx-ide-odtu.git>``` 
```cd mplabx-ide-odtu```

2. Build the Docker images:

```docker-compose build```

3. Run the containers using Docker Compose:

```docker-compose up```

MPLAB X IDE and PICSimLab should now be running in separate containers, connected via virtual serial ports using tty0tty.

## Usage

1. Open MPLAB X IDE and create or load a project.
2. Compile the project to generate a HEX file.
3. Open PICSimLab and load the HEX file to simulate the microcontroller.
4. Connect the virtual serial ports in MPLAB X IDE and PICSimLab to enable serial communication between the two applications.

Enjoy your development and simulation environment!

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update the documentation as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)
