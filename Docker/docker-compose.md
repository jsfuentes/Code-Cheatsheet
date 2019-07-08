# Docker-compose

Used to run multiple containers on same host

Outdated better to use docker stack/kubernetes now apparently

## Setup

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

## Commands

| Cmd                                   | Effect              |
| ------------------------------------- | ------------------- |
| docker-compose up                     | Run containers      |
| docker-compose build                  | Build containers    |
| docker-compose exec {service name} sh | Enter service shell |


