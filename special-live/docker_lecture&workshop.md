# Docker

## Virtual Machine (VM)
![Image](https://drive.google.com/uc?id=1m-RDktAgQiiIGS_OQSwdFeVCLC1t_CGc)

VMs were developed to solve the problem of deploying programs in a traditional way.
A single server can be used to run one application or multiple applications, but all resources must be shared. However, applications may use different programs, such as different versions of Python. Therefore, virtualization is the process of creating a virtual machine on a server so that they can be separated without sharing resources, such as CPU and RAM.

## Docker
![Image](https://drive.google.com/uc?id=1hxq_S5M62qni4oAeEJNA6D1s6Y55eq_Q)

Docker is OS-level virtualization
Docker = A single server can be used to run multiple applications, but each application can share components and resources.

**Container and VM**
![Image](https://drive.google.com/uc?id=1D3Sgl2RB7ldiwb4cqrUrF8DdeD55_a90)

Containers will run on a container management system. Docker shares the same operating system (OS).
VMs will use resources (CPU, RAM) by using a technology called "hypervisor" to simulate hardware. Each VM has its own operating system.

## Summary
Deployment Comparison

![Image](https://drive.google.com/uc?id=1splV3gH8ZwAGnvy1CabohSTLZ0nhuoLq)

## Docker Concept
**Build once, Run anywhere**

![Image](https://drive.google.com/uc?id=1axwfEv0WR11NB-Pf1PAjX2C9bWQ_Irmr)

**Container vs Image**
- Docker file: A text file that specifies the components that are needed to create a container image.
- Container image or Image: A file that contains the components specified in a Docker file. It is used to create a container.
- Docker container: A container that is used to run an application.

**Build**
Creating a container image from a Docker file gathers the required files and installs all required dependencies. The result is a container image that can be used in the next step.
**Run**
Creating container from image for running an application from image on our server. Can put an argument to กำหนด option such as name, container, port or command.
**Share**
Same as git. We need somewhere to store our works. It's called Container Registry.

## Basic Docker
Open docker engine and terminal

Try
```
docker run hello-world
```

![Image](https://drive.google.com/uc?id=1Nnl0yxJpTmhW1b8IxyBJGsTLIoNEljxV)

**Docker ps**
to show container that is running
ps -a means show all

```
docker ps -a
```

container id, Docker will randomly generate.
container name: If you do not specify the --name, Docker will generate a random name.

**Docker inspect**
The command used to view a container in detail. The result will be in .json format.

```
docker inspect <container_id>
```

![Image](https://drive.google.com/uc?id=1ShJxNjv9WXTvbk64dD6Ph6jEQAZ_Xx6b)

**Docker pull**
The command that use for pull (download) docker image from docker registry.

```
docker pull <container_image>:<tag>
```

tag : is a way to identify an image version for a container.

try pull Python

![Image](https://drive.google.com/uc?id=1fvtY-sCGed8EjhzsgHWhj6W01TgRSlH8)

**Docker images**
The command that use for list all image.

```
docker images
```

![Image](https://drive.google.com/uc?id=1xEVHgGttO4DahUyuKkKIjh3bpltkvbrD)

**Create Dockerfile**
Example of dockerfile
```
FROM python 3.11
COPY . /app
WORKDIR /app
RUN pip install --no--cache-dir \
    -r requirement.txt
CMD ["python", "app.py"]
```

FROM: The base image to use when creating the container.
COPY: Copies files from the host machine to the container. The . symbol refers to the current directory, so the COPY . /app instruction will copy all files from the current directory to the /app directory in the container.
WORK: The working directory for the container. This is the directory that will be used as the default starting directory when the container starts.
RUN: Runs a command in the container. This command is used to install packages or perform other tasks that need to be done before the container starts.
CMD: The command that will be run when the container starts. This command is typically used to start the application that is running in the container.

**Docker build**
Build command is the command that is used to build docker image from dockerfile

```
docker build -t <image_name>:<tag> .
```
dot(.) is for specify context to search for dockerfile only in this directory

**try use this repo**
use git clone to clone repository. Then use cd command to go into directory and use ls command to check file.

![Image](https://drive.google.com/uc?id=1FIjXS7H6W9LicMbcWjD6z1bvpCBQg9VO)

try to build

![Image](https://drive.google.com/uc?id=1dY7X7J7uWIlyAOU8Mpq6cO37KtSwf0Pl)

**Docker login & Docker push**
```
docker login [registry]
```

push command is uploading command that upload docker image to the registry. In case of not speficy name it will be pushed to Dockerhub
```
docker push <image_name>:tag
```

![Image](https://drive.google.com/uc?id=1Kx0r8fapcx3H4GoTjxPmo9x3RCc6M44q)

it will show on our registry
![Image](https://drive.google.com/uc?id=1VM5mhNjvITsNqEgjy1HGDm8-8A1ji9Mx)

**Docker run**
Run command is the command for creating container and run (create + start), including pull in case of image not found.

Run command have a lot of argument. Can see total option by using --help
```
docker run --help
```

Basic for docker run (simple version)
```
docker run <image_name>:<tag>
```

```
docker run [--name] [-d] [-p] [-v] <image_name>:<tage> [extra command]
```

  - --name<name> : insert container name
  - -d run : in background (daemon). It will not show log.
  - -p <host_port>:<container_port> : setting up port.
  - -v <host_path>:<container_path> : mounting (connecting with where to store container file)

![Image](https://drive.google.com/uc?id=1ux1pA8PlK3_ho7aUGSz83lRXYvZ40xHC)

Try run container that is used other's image.
try "Pokemonsay" (print message with pokemon picture)

![Image](https://drive.google.com/uc?id=19Vaz1EQe_2sq0uf-lrbdc6x3nhUtlqGh)

  - -rm : delete container imediately after run

**Docker start/stop/restart**
stop command is stopping container but container won't be deleted
```
docker stop <container_id(s)>
```

![Image](https://drive.google.com/uc?id=1qFJ8rEV2W9TugLTJRgDrUgG2JMGk61kH)

Start command is only using with stopped container
```
docker start <container_id(s)>
```

![Image](https://drive.google.com/uc?id=1CX_cQb_8EgRyiD-UCh2WCYM9yF30jG7i)

restart continer
```
docker restart <container_id(s)>
```

![Image](https://drive.google.com/uc?id=1f2G66GKMogMqO-PtELZxfdMNrRDELpE_)

**Docker logs**
It's the command that print all of log from the start. If only want it to print last 100 logs. use --tail 100

In case want log continuously, use -f (follow). It will print running container log as real-time.

```
docker logs [-f] [--tail n] <container_id>
```

**Docker rm & Docker rmi**
rm command is for deleting stopped container. In case want to remove running contain. add -f (force)

```
docker rm [-f] <container_id(s)>
```

![Image](https://drive.google.com/uc?id=1pV7yxW__wM2d3KjeIhHLMXj08U4_Cvp0)

rmi command is for removing unused image.
```
docker rmi [-f] <image_id(s)>
```

remove image "hello_world"

![Image](https://drive.google.com/uc?id=1daK-5EtvS1Gf8q7TUF2M6-QS0Pt0PLWV)

remove all of not in use images
```
docker system prune
```

**Docker network**
"Docker can create a virtual network that is shared by containers. Normally docker will create bridge network for all container. But you can create it on your own.

```
docker network create <network_name>
```
Then run with this command for ระบุ network
```
docker run --network=<network_name>
```

Docker network types
  - bridge (default)
  - Host:Docker : it will use network and port same as host (No network isolation).
  - Macvlan : For container that need MAC address for using with physical tools.
  - None : No network connection.

**Docker volume**
Docker volume is one of the ways to store files in Docker.

volume concept is create void space and link with container. Volume can be shared with multiple container.

Create volume
```
docker volume create <volume_name>
```

Use volume
```
docker run -v <volume_name>:<cotainer_path>
```

**Docker exec**
exec command is for run additional command on running container.

Most famous option
-it : it will make exec command be interactive. ไม่จบที่ one command.

famous command is "/bin/bash". This command is like shell(SSH).

```
docker exec [-it] <container_id(s)> <command>
```

![Image](https://drive.google.com/uc?id=1mCmEDi37Cku53Lpv79xH6kecatWFyrjB)

**Docker restart policy**
The run command can specify a restart policy when Docker has a problem or the machine suddenly shuts down. Have option "no | on-failure | always | unless-stopped"

Set up policy when run
```
docker run --restart=<restart policy> ...
```

Set up policy from updating after run
```
docker update --restart=<restart policy> <container_id>
```

**Summary Docker Basic Command**
- Create image from dockerfile : docker build
- Create container from image : docker run
- List image : docker images
- List all container : docker ps -a
- Inspect container detail : docker inspect
- download image : docker pull
- upload image : docker push
- start/stop/restart : docker start/stop/restart
- Remove image : docker rmi
- Remove all of not in use images : docker system prune
- remove container : docker rm
- run command via container : docker exec (-it)

**Mount docker**
Mount = Connect docker container with our storage
There are 3 types of mounting docker
1. Volume : Create new storage for docker (Docker recommend this).
2. Bind Mount : Connect docker with folder or files on the machine that runs docker.
3. Tmpfs (Temporary File System) Mount : Create temporary storage on machine's memories. It will be disapeared if stop container.

*Beware of bind mount. Do not mount home or root directly because docker will have all access to your computer.*

**Docker restart policy**
According to above topic docker restart policy. There are 4 types of setting restart policy
1. restart = No
  - Don't automatically restart
2. restart = Always
  - When program finished. Docker will be keeping restart.
  - Container will be opened with our computer. It will waste resource.
3. restart = Unless-stopped
  - When program finished. Docker will be keeping restart.
  - Unless computer turn on or turn off. Container won't be opened.
4. restart = On-failure
  - Restart when Docker container got an error.

## Docker Compose & Kubernetes
Pain point of using Docker is when to use container. Container must be ordered each one at a time. This makes it difficult to connect between container.
So **Docker compose** was created. It can turn on and off all of container in 1 command.

**docker-compose.yml**

Command to use docker-compose after created docker-compose.yml
```
docker-compose up
docker-compose down
```
Or command for start or stop for a while.
```
docker-compose start
docker-compose stop
```

**Workshop**

Link example to docker workshop : https://github.com/woraperth/docker-workshop

try docker compose command

docker compose up -d to run in background and use docker compose down to stop all of the containers

![Image](https://drive.google.com/uc?id=1eNqs0rcb-wzjlU5roGb-74Ru-tmhR-57)

**Kubernetes**

- open source that is developed by Google
- Kubernetes is for managing the container (Container Orchestration) = helps manage application.
- Can create cluster (servers) both on on-premise and Cloud.

Container Orchestration Engine

![Image](https://drive.google.com/uc?id=1QRrs08JI3Obq06QUIUZm7tEu25HlVgnI)

Features
1. Manage containers (pods) - Create and deploy containers.
2. Self-healing - In case of containers got a problem, Kubernetes can create new containers immediately.
3. Auto-scale - Can automatically scale.
4. Service discovery - Help find other services. easy to connect.
5. Load balancing - Manage traffic, reduce hotspot.
6. Secret management - Manage secret in the system e.g. password.

Kubernetes Architecture

![Image](https://drive.google.com/uc?id=1OH3yJe6nffyFDbSxP8-9OoscOon5OVaD)

**Docker & Kubernetes**
Kubernetes can work with container image that are created by Docker. So we can work locally by using docker and also can work in cluster level in case using Kubernetes.
Moreover, Kubernetes can work with other container creators like Docker, Containerd, and Podman.

**Airflow on Docker**
Airflow on docker is docker image that can be downloaded and used from dockerhub. 

Why we need to use Airflow on Docker instead of using Cloud Composer?
1. Cloud Composer is too expensive.
2. Can use new version of Airflow.
3. Airflow on Docker is for Local development.

1. Airflow
Before begin. I follow these step : https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html
  - fetch docker-compose.yaml from these
  ```
  curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.7.1/docker-compose.yaml'
  ```
  - make dir and create .env file
  ```
  mkdir -p ./dags ./logs ./plugins ./config
  echo -e "AIRFLOW_UID=$(id -u)" > .env
  ```
  - then run this on bash command
  ```
  docker compose up airflow-init
  ```

  - next run docker compose up

  Server is created as port 8080

2. Airflow with environment variables
Why need environment variables? because It for keeping password file.