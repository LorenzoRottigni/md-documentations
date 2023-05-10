# DOCKER - basics

Docker is a "virtual boat" that creates a virtual network on a localhost or on a server.
By creating the virtual network, Docker allows you to expose services on ports of the virtual network instaed of public ports.

Docker uses images to create and run containers containing a service.
Images are seqeunces of instructions to start a service.

On Docker Virtual Boat you can add many containers, each containing one running service.
A Docker container is created and started by running instructions contained in a docker image.

## Install Docker on Ubuntu Server

### Unistall old Docker istances:

` sudo apt-get remove docker docker-engine docker.io containerd runc `

### Install Docker

```
sudo apt-get update
sudo apt-get upgrade
audo apt-get install docker
```

