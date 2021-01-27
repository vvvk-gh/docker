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

sudo dockerd        # it's docker deamon and it should be always running in a seperate tab.

sudo docker version  # to verify installation
```

### Getting Started

1. Running a container

```cmd
sudo docker container run hello-world
```

output :

```cmd

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```

#### What happend internally when you run tha above command ?

```
    sudo docker container run <docker-image-name>
```

When ever you try to run above it checks for the docker-image containing a matching name locally, if not searches in the docker repository online (Docker Hub) and downloads it and forms a container and executes it.

### Starting a shell

```bash
# alpine is very minimal linux distribution (few MB in size) best for docker
# you want to execute inside the container we use word shell 'sh'
# whenever you start an interactive program like shell inside a container we need to use flags "-it"

 ❌ sudo docker container run alpine sh      # wont work

 ✅ sudo docker container run -it alpine sh

cat /etc/os-release                     # to check whether we are inside alpine
uname -r                                # gives you the name of the kernal

# it will same as your original kernal even though you are inside a container.
# docker is just a process on your os it wont be having a new kernal like VM's

```

`Task 1` : Just like alpine run centos in a shell

```cmd
    sudo dockerd                            # starting docker deamon if it's stopped already.
    sudo docker container run -it centos
    cat /etc/os-release                     # to verify whether we are inside centos
    uname -r                                # to verify kernal (same as original)
```

---

## New containers , Existing Containers

Everytime you use a command

```
docker container run <image>
```

it create a new container but to use the existing one using `attach`.
Let's check how

### ls

```
sudo docker container ls       # lists all the active container
sudo docker container ls -a    # lists all the active and disactive container
```

### start , stop

```
docker container start <container_name>   # starts the container
docker container stop <container_name>    # stops the container
```

### Terminate container , attach , detach

Everytime you press `ctrl+d` the container terminates

insider : when ever you press `ctrl+d` it terminates the container as shell the main process of the container, the shell will also terminate along with it.

```terminal
    sudo container run -it alpine sh
    pressed `ctrl+d`
    sudo docker container ls
    will output nothing as we terminated the container
```

Now try running a container and press `ctrl+p` and `ctrl+q`

```
sudo docker container run -it alpine sh

pressed `ctrl+p` and `ctrl+q`

sudo docker container ls

CONTAINER ID   IMAGE     COMMAND   CREATED         STATUS         PORTS     NAMES
34295b155e1c   alpine    "sh"      8 minutes ago   Up 2 seconds             sharp_kalam

```

when you click `ctrl+p` and `ctrl+q` the container is just detached and your cursor will be moved to your local machine.

but the container runs in the background

you can reattach to it using below

```
sudo docker attach <container_name>
```

what if you want to use same container that is already terminated and you dont want to create new one ?

```
sudo docker container ls -a                     # list of active and exited
sudo docker start <container_name>              # select the container_name that you want to use
sudo docker attach <container_name>             # attaches to the previous container

# verify with hostname (before and after hostname should be same)
```
