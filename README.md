# provoice-build-rtpengine
ProVoice packages build environment for rtpengine using Docker

## About

This project aims to make reproducable Debian packages of rtpengine for Ubuntu 20.04 LTS by using Docker. We have chosen to use upstream MySQL packages instead of the default packages in the Ubuntu repository. Feel free to remove these lines in the Dockerfile if that would fit your environment better. Create an empty directory for the packages and run the container to build the Debian packages.

In this build we are removing the `ngcp-` prefix for the packages and file names. The `debian` source files in the `bcg729` package have been copied from the `bcg729` package in the Ubuntu repository. Version numbers for the packages have to be set through environmental variables while running the Docker container.

rtpengine is part of the [ProVoice platform](https://provoice.eu).

## Building the packages

1. Clone the repository, initialize the Git submodules and build the Docker image
```bash
git clone https://github.com/ProVoice/provoice-build-rtpengine.git
cd provoice-build-rtpengine
git submodule init
git submodule update --remote
sudo docker build -t provoice-build-rtpengine .
```
2. Create a directory for the packages
```bash
mkdir packages
```
3. Run the container to build the packages
```bash
sudo docker run -it \
 --rm \
 -v `pwd`/packages:/app/packages \
 -e BCG729_VERSION='1.1.1' \
 -e RTPENGINE_VERSION='9.3.2.0' \
provoice-build-rtpengine
```
The packages and source files should now be in the `packages` directory and ready to install on Ubuntu 20.04 LTS.
