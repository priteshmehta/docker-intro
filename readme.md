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

#### Pull the docker image from docker registry 

```
docker pull nginx

// Other options

docker pull nginx:<Tag>
docker pull myregistry.local:5000/testing/test-image
docker pull ubuntu@sha256:45b23dee08af5e43a7fea6c4cf9c25ccf269ee113168c19722f87876677c5cb2

```

---

#### To list locally available docker images

```
docker images
docker images -a

```

---

#### To List running conainers

```
docker ps
docker ps -a 

```

---

#### Run the container

```
docker run -d -p 9090:80 --name webservice1 nginx
docker run -d --name ubuntu ubuntu:16.04 tail -f /dev/null

```


---

#### Copy content into the conainer


###### Copy file(s)/folder

```
docker cp sample_html/index1.html webservice1:/usr/share/nginx/html/

```
###### Mount the local folder

```
docker run -d -p 5000:80 -v ~/nginxlogs:/var/log/nginx --name webservice2 nginx

```

---

#### Access Docker Container 

```
docker exec -it webservice1 bash
docker exec webservice1 service nginx stop
docker logs --follow webservice1

```

---

#### Remove Containers & Images

```

docker stop/start/restart [CONTAINER]
docker rm [CONTAINER]
docker images purge
docker images [IMAGE]
docker volume rm  [VOLUMNE_NAME]

```

---

#### Other Useful Commands

```

docker top [CONTAINER]
docker port [CONTAINER]
docker inspect [CONTAINER]
docker network ls
docker volume ls
docker stats
docker help 
docker info
docker version
docker kill 

```

---


### The Dockerfile

> A Dockerfile is a text document that contains all the commands a user could call on the command line to create an image.

#### Sample Dockerfile

- Dockerfile For above example:  [Click Here](https://github.com/priteshmehta/docker-intro/blob/master/Dockerfile)
- Dockerfile with inline comments: [Click Here](https://github.com/priteshmehta/docker-intro/blob/master/examples/dockerfile/Dockerfile)


---


### Build using Dockerfile

```
docker build .
docker build -t webservice2:1 -f [DOCKERFILE]
docker push webservice2:1

```

---

### Questions?

![questions!](https://raw.githubusercontent.com/priteshmehta/docker-intro/master/img/3d_question_guy.png)


---

### Kubernetes


![Kubernetes logo](https://avatars1.githubusercontent.com/u/13629408?s=400&v=4)

---

### What is Kubernetes?

- Kubernetes is a "Container Orchestrator" or "Cluster Manager".
- Basic monitoring, logging, health checking
- Enables containers to find each other.


---

### Kube Cluster

![Kubernetes cluster](https://github.com/priteshmehta/docker-intro/blob/master/img/kube_arch.png?raw=true)

---


### Important Terminology

- Pod
- ReplicaSet (old name ReplicationController)
- Service
- Deployment  
- ingress (a.k.a L7 Load balancer)

---

### Basic Usage

- Deploy a containerized application on a cluster
- Scale the deployment
- Update the containerized application with a new software version
- Debug the containerized application

---

### Create Kube Cluster

![Kube Cluster](https://d33wubrfki0l68.cloudfront.net/99d9808dcbf2880a996ed50d308a186b5900cec9/40b94/docs/tutorials/kubernetes-basics/public/images/module_01_cluster.svg)

```
minikube version
minikube start
minikube addons list

```

```
kubectl version
kubectl cluster-info
kubectl get nodes
```

---


### Deploy App in Kube Cluster

![Deploy app](https://d33wubrfki0l68.cloudfront.net/152c845f25df8e69dd24dd7b0836a289747e258a/4a1d2/docs/tutorials/kubernetes-basics/public/images/module_02_first_app.svg)

```

kubectl run kube-demo-service --image=nginx:latest --port=9091
kubectl get pods
kubectl get rs
kubectl get deployments
kubectl exec -it [POD] bash
kubectl logs [POD]

```

---

### Create Service

![diagram](https://d33wubrfki0l68.cloudfront.net/cc38b0f3c0fd94e66495e3a4198f2096cdecd3d5/ace10/docs/tutorials/kubernetes-basics/public/images/module_04_services.svg)

```

kubectl expose deployment/kube-demo-service --type="NodePort" --port=80
kubectl get services
kubectl describe services/kube-demo-service

```

---


### Expose to Public (load Balancer)


```

minikube addons enable ingress
kubectl create -f [ResourceFile]
kubectl get ing

```

---

### Scalling App

```
kubectl scale deployments/kube-demo-service --replicas=4
kubectl get deployments
kubectl get pods -o wide

```

---

### Rolling Update


![kube rolling update](https://github.com/priteshmehta/docker-intro/blob/master/img/kube_rolling_update.gif?raw=true)

```
kubectl describe pod [PODNAME]
kubectl set image deployments/kube-demo-service kube-demo-service=kube-demo-service:v2
kubectl describe services/kube-demo-service

````

---

### Cleanup

```

kubectl delete deployment kube-demo-service
kubectl delete service kube-demo-service
minikube stop
minikube delete

```

---

### Misc commands

```
kubectl proxy
kubectl exec -ti $POD_NAME curl localhost:8080
kubectl exec -ti kube-demo-service-7bc677bf86-6zkrn curl localhost:9091
curl http://localhost:8001/version
curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME
kubectl edit -oyaml deployment kube-demo-service
eval $(minikube docker-env)

```
