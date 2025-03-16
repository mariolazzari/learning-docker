# Learning Docker

## Docker explained

Docker uses images and container to deploy applications consistently.

### Virtual machines vs Containers

- Virtual machines use hypervisors to emulate real hardware
  - lots of space
  - install new os
  - run multiple apps
  - cannort interact their hosts
  
- Containers do not emulate hardware 
  - No boot needed
  - no os needed
  - much less space
  - run one app only
  - can interact with their hosts

### Anatomy of a container

- limits what you can see
- limits what you can use

### Docker

- **Dockerfiles** simplify configuration and packaging
- **Docker hub** shares images
- **Docker Cli** starts container

## Docker desktop

- Virtual box Linux VM with docker only
- Handles volumes and ports
- User interface

### Installation

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install --cask docker
docker run --rm hello-world # remove container after execution 
docker ps
```

## Using Docker

### Docker Cli

```sh
# show all docker commands
docker --help 
# show all command options
docker network --help
# show all option values
docker network create --help
```

#### Create container

```sh
# long way
docker container create --help
# creates but does not run
docker container create hello-world:linux 
# show running containers only
docker ps
# show all containers
docker ps --all
docker ps -a
# start container
docker container start CONTAINER_ID
# show container logs
docker container logs CONTAINER_ID
# attach termonal to container
docker container start --attach CONTAINER_ID

# short way: docker run = create + start + attach
docker run hello-world
```

#### Dockerfile

```
FROM ubuntu

LABEL maintainer="Carlos Nunez <dev@carlosnunez.me>"

USER root

COPY ./entrypoint.bash /

RUN apt -y update
RUN apt -y install curl bash
RUN chmod 755 /entrypoint.bash

USER nobody

ENTRYPOINT [ "/entrypoint.bash" ]
```

```sh
docker build -t first-image .
docker run first-image
```

#### Container interactions

```sh
docker build --file server.Dockerfile --tag first-server .
# detach container
docker run -d first-server
# exec command in container
docker exec ID date
# interact with container
docker exec -it ID bash
# stop containr
docker stop ID
# remove container
docker rm ID
# show images
docker images
# remove image
docker rmi ID
```

#### Binding ports & name

```sh
docker build --file web-server.Dockerfile --tag web-server .
docker run -d --name web-server -p 5001:5000 web-server 
```

#### Container data: volumes

```sh
docker run --rm --entrypoint sh -v /tmp/container:/tmp ubuntu -c "echo 'Ciao Mario' >/tmp/file && cat /tmp/file"
```

### Docker Hub

```sh
# tag image
docker tag web-server mariolazzari/web-server:0.0.1
# push image to docker hub
docker push mariolazzari/web-server:0.0.1
```

#### Challenge

```sh
docker run --name webserver -v ./website:/usr/share/nginx/html -p 5000:80 --rm nginx
```

## When something goes wrong

### Out of space

```sh
# show all images
docker images
# remove image
docker rmi ID
# remove all
docker system prune
```

### Slow container

```sh
# container stats
docker stats CONTAINER_ID
# ex
docker run --name=alpine --entrypoint=sleep -d alpine infinity
docker exec -it alpine sh
yes
# inspect
docker inspect CONTAINER_ID
docker top CONTAINER_ID
```