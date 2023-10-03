# Containerized QT development environment

This repository contains a QT sample app within a containerized development environment in vscode. With this you can develop QT apps easily.

Docker base image contains QT 6.5.2 build from sources.

## Prerequisites

- VSCode with Dev Containers extension installed
- Docker
- Nvidia container toolkit and runtime
  
Tested in Ubuntu 20.04

## Setup

Follow the steps here to install all prerequisites.

### VSCode

1. Download and install VSCode (https://code.visualstudio.com/download)
2. Install Dev Containers extension (https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Docker

1. Install docker and follow the instructions from here: https://docs.docker.com/engine/install/ubuntu/
2. Follow the post installation steps here: https://docs.docker.com/engine/install/linux-postinstall/

### Nvidia container toolkit

1. Follow the instructions from here: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html
2. Check if installation is working with steps described here: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/sample-workload.html

## Usage

Clone the repository:

```clone
git clone 
```

Build the base image that contains QT 6.5.2:

```build base image
cd QTSampleApp/.decvontainer
./build_base_image.sh
```

This will take same time because it compiles QT.

Open the container in VSCode:

```OpenVSCode
code QTSampleApp
```

Press the button that open with "Reopen in container" or press CTRL+SHIFT+P and search for "Dev Containers: Reopen in Container"

Build the sample app from project folder:

```Build
cmake -S src -B build && cmake --build build
```

To build in debug mode run:

```BuildDebug
cmake -DCMAKE_BUILD_TYPE=Debug -S src -B build && cmake --build build
```

