# Docker

## Day 1 :

### What is docker ?

- It is a piece of technology that helps you develop , deploy and running your application using container technology.

- It has all the application code + its dependencies packed to together

- Portable and also executable anywhere like cloud or any laptop.

### What are containers ?

- Packages that holds the application code along with its dependencies are called container images

- When you execute this images you get a container.

- At the end containers are just the processes on OS. But as the docker takes care of running containers so process are in isolation (have their own network , file system so..on).

### Containers vs Virtul machine's (vm's)

- VM's achieve isolation on the hardware level which means
  it will slice the ram, disks, cpu's into pieces and it wil assign slice of it to a new vm and we will install new os and applications in it and use it.

- Containers are just processes in an OS , isolation is achieved by from the features of the kernal of this OS.

- Vm are heavy (own OS + own kernal + bunch of baggage you may not use)
  containers are light weight (no boot process + only useful for your application)

### Types of Docker Containers

1. Windows Containers
2. Linux Containers

As it docker run containers using OS kernal,ends up having two different types of containers.

## Day 2 :

### Installing Docker

```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo docker run hello-world


```
