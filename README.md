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