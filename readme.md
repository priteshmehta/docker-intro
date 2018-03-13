![Docker logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_logo.png)

## Docker - Introducation

________________________


###### Under [Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/) license.

---


### What is Docker?

> Docker is an open platform for developing, shipping, and running applications.

> Docker allows you to package an application with all of its dependencies into a standardized unit for software development.

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

###### See the [survey results for 2016](https://www.docker.com/survey-2016)

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

![Docker architecture](https://docs.docker.com/engine/images/architecture.svg)
###### See more at [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

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

### Steps of a Docker workflow

```
docker run -i -t -d ubuntu:15.04 /bin/bash
```

 - Pulls the ubuntu:15.04 [image](https://docs.docker.com/engine/userguide/containers/dockerimages/ "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot.") from the [registry](https://docs.docker.com/registry/ "The central place where all publicly published images live. You can search it, upload your images there and when you pull a docker image, it comes the repository/hub.")
 - Creates a new [container](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/ "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides.")
 - Allocates a filesystem and mounts a read-write [layer](https://docs.docker.com/engine/reference/glossary/#filesystem "A set of read-only files to provision the system. Think of a layer as a read only snapshot of the filesystem.")
 - Allocates a [network/bridge interface](https://www.wikiwand.com/en/Bridging_%28networking%29 "")
 - Sets up an [IP address](https://www.wikiwand.com/en/IP_address "An Internet Protocol address (IP address) is a numerical label assigned to each device (e.g., computer, printer) participating in a computer network that uses the Internet Protocol for communication.")
 - Executes a process that you specify (``` /bin/bash ```)
 - Captures and provides application output

---

### The docker image

![ubuntu:15.04 image](https://docs.docker.com/storage/storagedriver/images/container-layers.jpg) "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot. Each Docker image references a list of read-only layers that represent filesystem differences. Layers are stacked on top of each other to form a base for a container’s root filesystem.")

---

### The docker container

![container using ubuntu:15.04 image](https://docs.docker.com/storage/storagedriver/images/sharing-layers.jpg) "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides. For each containers there is a new, thin, writable layer - container layer - on top of the underlying stack (image).")

---

### The Dockerfile

> A Dockerfile is a text document that contains all the commands a user could call on the command line to create an image.

 - [Dockerfile with inline comments](https://github.com/theodorosploumis/docker-presentation/blob/gh-pages/examples/dockerfile/Dockerfile) just for education
 - [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) on docker docs
 - Official Dockerfiles ([rails](https://github.com/docker-library/rails/blob/master/Dockerfile), [nodejs](https://github.com/ReadyTalk/nodejs-docker/blob/master/base/Dockerfile), [django](https://github.com/docker-library/django/blob/master/3.4/Dockerfile), [Drupal](https://github.com/docker-library/drupal/blob/master/8.1/fpm/Dockerfile))

---

### Common Docker Commands

```
// General info
man docker // man docker-run
docker help // docker help run
docker info
docker version
docker network ls

// Images
docker images // docker [IMAGE_NAME]
docker pull [IMAGE] // docker push [IMAGE]

// Containers
docker run
docker ps // docker ps -a, docker ps -l
docker stop/start/restart [CONTAINER]
docker stats [CONTAINER]
docker top [CONTAINER]
docker port [CONTAINER]
docker inspect [CONTAINER]
docker inspect -f "{{ .State.StartedAt }}" [CONTAINER]
docker rm [CONTAINER]

```

---

### Example: SSH into a container

```
docker pull ubuntu
docker run -it --name ubuntu_example ubuntu /bin/bash
```

---

### Example: Build an Image

Let's build a [jenkins image](https://github.com/komljen/dockerfile-examples/blob/master/jenkins/Dockerfile)

```
cd ~/Docker-presentation
git clone git@github.com:komljen/dockerfile-examples.git.git
cd dockerfile-examples/jenkins
docker build -t jenkins-local .

// Test it
docker run -d -p 8099:8080 --name jenkins_example jenkins-local
// Open http://localhost:8099
```

---

### Example: Docker volume

Let's use [Apache server](https://bitbucket.org/EdBoraas/apache-docker/src/)

```
cd ~/Docker-presentation
mkdir apache-example
cd apache-example

docker pull eboraas/apache
docker run --name apache_volume_example \
           -p 8180:80 -p 443:443 \
           -v $(pwd):/var/www/ \
           -d eboraas/apache

// Locally create an index.html file
mkdir html
cd html
echo "It works using mount." >> index.html

// Open http://localhost:8180 to view the html file
```

---

### Example: Docker link containers

Let's create a [Drupal app](https://hub.docker.com/_/drupal/) (apache, php, mysql, drupal)

```
cd ~/Docker-presentation
mkdir drupal-link-example
cd drupal-link-example

docker pull drupal:8.0.6-apache
docker pull mysql:5.5

// Start a container for mysql
docker run --name mysql_example \
           -e MYSQL_ROOT_PASSWORD=root \
           -e MYSQL_DATABASE=drupal \
           -e MYSQL_USER=drupal \
           -e MYSQL_PASSWORD=drupal \
           -d mysql:5.5

// Start a Drupal container and link it with mysql
// Usage: --link [name or id]:alias
docker run -d --name drupal_example \
           -p 8280:80 \
           --link mysql_example:mysql \
           drupal:8.0.6-apache

// Open http://localhost:8280 to continue with the installation
// On the db host use: mysql

// There is a proper linking
docker inspect -f "{{ .HostConfig.Links }}" drupal_example
```

---

### Example: Using Docker Compose

Let's create a Drupal app with [docker-compose.yml](https://github.com/theodorosploumis/docker-presentation/blob/gh-pages/examples/docker-compose/docker-compose.yml)

```
cd ~/Docker-presentation
git clone git@github.com:theodorosploumis/docker-presentation.git
cd docker-presentation/examples/docker-compose

// Run docker-compose using the docker-compose.yml
cat docker-compose.yml
docker-compose up -d
```

---

### Example: Share a public Image

```
cd ~/Docker-presentation
git clone git@github.com:theodorosploumis/docker-presentation.git
cd docker-presentation

docker pull nimmis/alpine-apache
docker build -t tplcom/docker-presentation .

// Test it
docker run -itd --name docker_presentation \
           -p 8480:80 \
           tplcom/docker-presentation

// Open http://localhost:8480, you should see this presentation

// Push it on the hub.docker.com
docker push tplcom/docker-presentation
```

---


### The Docker war

| Type | Software |
|:----:|----------|
| Clustering/orchestration | [Swarm](https://docs.docker.com/swarm/), [Kubernetes](http://kubernetes.io/), [Marathon](https://mesosphere.github.io/marathon/), [MaestroNG](https://github.com/signalfx/maestro-ng), [decking](http://decking.io/), [shipyard](http://shipyard-project.com/) |
| Docker registries | [Portus](http://port.us.org/), [Docker Distribution](https://github.com/docker/distribution), [hub.docker.com](http://hub.docker.com), [quay.io](https://quay.io), [Google container registry](https://cloud.google.com/tools/container-registry/), [Artifactory](https://www.jfrog.com/artifactory/), [projectatomic.io](http://www.projectatomic.io/) |
| PaaS with Docker | [Rancher](http://rancher.com/), [Tsuru](https://tsuru.io/), [dokku](https://github.com/dokku/dokku), [flynn](https://flynn.io/),  [Octohost](http://octohost.io/), [DEIS](http://deis.io/) |


---

###Time to get your hand dirty....

[Gify]


---


### Deploy microservice using Docker

1. Pull the docker image from docker registry 

```
docker pull nginx

// Other options

docker pull nginx:<Tag>
docker pull myregistry.local:5000/testing/test-image
docker pull ubuntu@sha256:45b23dee08af5e43a7fea6c4cf9c25ccf269ee113168c19722f87876677c5cb2

```

2. Check if docker image is locally available

```
docker images
docker images -a

```

3. Check total conainers running at this moment

```
docker ps
docker ps -a 
```

4. Run the container

```
docker run -d -p 9090:80 --name webservice1 nginx

// Other useful options
docker run -d -p 9090:80  -v nginx-vol:/usr/share/nginx/html --name webservice2 nginx
docker run -d --name ubuntu ubuntu:16.04 tail -f /dev/null
```


---

### Copy files in to conainer

```
1. Copy files

docker cp [FILEA|DIR] [CONTAINER]:/usr/share/nginx/html/
e.g. docker cp ./index1.html webservice1:/usr/share/nginx/html/

2. Mount the local folder

```


---

### Access container 

```

docker exec -it [CONTAINER] /bin/bash

docker exec [CONTAINER] <cmd>
For Example: 
   docker exec webservice1 service nginx stop
   docker exec webservice1 tail -f 

docker logs --follow webservice1

```

---

### Remove container/images

```

docker stop/start/restart [CONTAINER]
docker rm [CONTAINER]
docker images purge
docker images [IMAGE]

```

---

### Miscellaneous useful commands

```

docker top [CONTAINER]
docker kill 
docker stats
docker help 
docker info
docker version
docker network ls

```

---


### Questions?

![Pythons over Docker!](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_logo.png)
http://make-anything.wikia.com/wiki/File:3d_question_guy.png

---
