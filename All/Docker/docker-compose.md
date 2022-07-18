# Docker-compose

Used to run multiple containers on same host

Outdated better to use docker stack/kubernetes now apparently

## Commands

| Cmd                                   | Effect              |
| ------------------------------------- | ------------------- |
| docker-compose up                     | Run containers      |
| docker-compose build                  | Build containers    |
| docker-compose exec {service name} sh | Enter service shell |

## Setup

The Compose file is a [YAML](http://yaml.org/) file defining [services](https://docs.docker.com/compose/compose-file/#service-configuration-reference), [networks](https://docs.docker.com/compose/compose-file/#network-configuration-reference) and [volumes](https://docs.docker.com/compose/compose-file/#volume-configuration-reference). The default path for a Compose file is `./docker-compose.yml`.

docker-compose.yml

```dockerfile
version: "3"
services:
  node_backend:
    build: ./backend
    ports: 
      - "3001:3001"
    volumes:
      - ./backend:/app
      
  react_frontend:
    build: ./client
    ports: 
      - "3000:3000"
    volumes:
      - ./client:/app
```

### Config Options

##### build

`build` can be specified either as a string containing a path to the build context

##### image

```
build: ./dir
image: webapp:tag
```

This results in an image named `webapp` and tagged `tag`, built from `./dir`.