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
```