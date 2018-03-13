![Docker logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_logo.png)

## Docker - Introduction

________________________


###### By Pritesh

---


### What is Docker?

- Docker is an open platform for developing, shipping, and running applications.

- Docker allows you to package an application with all of its dependencies into a standardized unit for software development.

---

### Docker vs VMs

![Docker vs traditional Virtualization](https://insights.sei.cmu.edu/assets/content/VM-Diagram.png)

---


### Docker Benefits

 - Fast (deployment, migration, restarts)
 - Secure
 - Lightweight (save disk & CPU)
 - Open Source
 - Portable software
 - Microservices and integrations (APIs)
 - Simplify DevOps
 - Version control capabilities

---

### Common Docker usages

 - Sandbox environment (develop, test, debug, educate)
 - Continuous Integration & Deployment
 - Scaling apps
 - Development collaboration
 - Infrastructure configuration
 - Local development
 - Multi-tier applications
 - PaaS, SaaS

---

### Technology behind Docker

 - Linux [x86-64](https://www.wikiwand.com/en/X86-64)
 - [Go](https://golang.org/) language
 - [Client - Server](https://www.wikiwand.com/en/Client%E2%80%93server_model) (deamon) architecture
 - Union file systems ([UnionFS](https://www.wikiwand.com/en/UnionFS): AUFS, btrfs, vfs etc)
 - [Namespaces](https://en.wikipedia.org/wiki/Cgroups#NAMESPACE-ISOLATION) (pid, net, ipc, mnt, uts)
 - Control Groups ([cgroups](https://www.wikiwand.com/en/Cgroups))
 - Container format ([libcontainer](https://github.com/opencontainers/runc/tree/master/libcontainer "Libcontainer provides a native Go implementation for creating containers with namespaces, cgroups, capabilities, and filesystem access controls. It allows you to manage the lifecycle of the container performing additional operations after the container is created."))

###### See more at [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

---

### The Docker architecture

![Docker architecture](http://19yw4b240vb03ws8qm25h366-wpengine.netdna-ssl.com/wp-content/uploads/Docker-API-infographic-container-devops-nordic-apis.png)

---

### Docker components

 - (Docker) client
 - daemon
 - engine
 - machine
 - compose
 - swarm
 - registry

---

### Docker Component Architecture

![Docker component architecture](https://docs.docker.com/engine/images/engine-components-flow.png)



---

### Docker client

It is the primary user interface to Docker. It accepts commands from the user
and communicates back and forth with a Docker daemon.

---

### Docker daemon

It runs on a host machine. The user does not directly interact with the daemon,
but instead through the Docker client with the RESTful api or sockets.

---

### Docker engine

A Client with a Daemon as also as the docker-compose tool. Usually referred simply as "docker".

---

### Docker machine

![Docker machine logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_machine.png)

A tool which makes it really easy to create Docker hosts on your computer,
on cloud providers and inside your own data center.
It creates servers, installs Docker on them, then configures the Docker client to talk to them.
Required for Mac, Windows users.

---

### Docker compose

![Docker compose logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_compose.png)

A tool for defining and running complex applications with Docker
(eg a multi-container application) with a single file.

---

### Docker swarm

![Docker swarm logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_swarm.png)

A native clustering tool for Docker. Swarm pools together several Docker
hosts and exposes them as a single virtual Docker host. It scale up to multiple hosts.

---

### Docker distribution

![Docker distribution logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_distribution.png)

A (hosted) service containing repositories of images which responds to the Registry API.

---

### The docker image

![ubuntu:15.04 image](https://docs.docker.com/storage/storagedriver/images/container-layers.jpg) 

- Each Docker image references a list of read-only layers that represent filesystem differences.
- Layers are stacked on top of each other to form a base for a container’s root filesystem.

---

### The docker container

![container using ubuntu:15.04 image](https://docs.docker.com/storage/storagedriver/images/sharing-layers.jpg) 
- A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides. 
- For each containers there is a new, thin, writable layer - container layer - on top of the underlying stack (image).


---


### Let's get started

![gif](https://media.giphy.com/media/JIX9t2j0ZTN9S/giphy.gif)

---


### Goal: Deploy microservice using Docker

#### Step1: Pull the docker image from docker registry 

```
docker pull nginx

// Other options

docker pull nginx:<Tag>
docker pull myregistry.local:5000/testing/test-image
docker pull ubuntu@sha256:45b23dee08af5e43a7fea6c4cf9c25ccf269ee113168c19722f87876677c5cb2

```
---

#### Step2: Check if docker image is locally available

```
docker images
docker images -a

```

---

#### Step3: Check total conainers running at this moment

```
docker ps
docker ps -a 

```

---

#### Step4: Run the container

```
docker run -d -p 9090:80 --name webservice1 nginx

// Other useful options
docker run -d -p 9090:80  -v nginx-vol:/usr/share/nginx/html --name webservice2 nginx
docker run -d --name ubuntu ubuntu:16.04 tail -f /dev/null

```


---

#### Step5: Copy content into the conainer

```

docker cp [FILEA|DIR] [CONTAINER]:/usr/share/nginx/html/
Example: docker cp ./index1.html webservice1:/usr/share/nginx/html/

2. Mount the local folder

Example: 

```

---

### Access Docker Container 

```

docker exec -it [CONTAINER] /bin/bash

docker exec [CONTAINER] <cmd>
For Example: 
   docker exec webservice1 service nginx stop
   docker exec webservice1 tail -f 

docker logs --follow webservice1

```

---

### Remove the Containers & Images

```

docker stop/start/restart [CONTAINER]
docker rm [CONTAINER]
docker images purge
docker images [IMAGE]

```

---

### Other Useful Commands

```

docker top [CONTAINER]
docker port [CONTAINER]
docker inspect [CONTAINER]
docker network ls
docker stats
docker help 
docker info
docker version
docker kill 

```

---


### The Dockerfile

> A Dockerfile is a text document that contains all the commands a user could call on the command line to create an image.

 - [Dockerfile with inline comments](https://github.com/theodorosploumis/docker-presentation/blob/gh-pages/examples/dockerfile/Dockerfile) just for education
 - [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) on docker docs
 - Official Dockerfiles ([rails](https://github.com/docker-library/rails/blob/master/Dockerfile), [nodejs](https://github.com/ReadyTalk/nodejs-docker/blob/master/base/Dockerfile), [django](https://github.com/docker-library/django/blob/master/3.4/Dockerfile), [Drupal](https://github.com/docker-library/drupal/blob/master/8.1/fpm/Dockerfile))

---

### Sample Dockerfile

```
[file content]

```

### Build image using Dockerfile

```
docker build .
docker build -f [DOCKERFILE]

```


### Questions?

![Pythons over Docker!](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_logo.png)
http://make-anything.wikia.com/wiki/File:3d_question_guy.png

---

### Kubernetes


![Kubernetes logo](https://avatars1.githubusercontent.com/u/13629408?s=400&v=4)

---

### Highlevel Architecure

![Kubernetes basic diragram](https://storage.googleapis.com/cdn.thenewstack.io/media/2016/11/Chart_04_Kubernetes-Node.png)


### Important Terminology

- Pod
- service

---

