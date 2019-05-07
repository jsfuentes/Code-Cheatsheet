# Docker-compose

Used to run multiple containers on same host

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

This `docker-compose.yml` file tells Docker to do the following:

## Commands

| Cmd                                   | Effect              |
| ------------------------------------- | ------------------- |
| docker-compose up                     | Run containers      |
| docker-compose build                  | Build containers    |
| docker-compose exec {service name} sh | Enter service shell |



| Cmd                                            | Effect                                           |
| ---------------------------------------------- | ------------------------------------------------ |
| docker stack ls                                | # List stacks or apps                            |
| docker stack deploy -c <composefile> <appname> | # Run the specified Compose file                 |
| docker service ls                              | # List running services associated with an app   |
| docker service ps <service>                    | # List tasks associated with an app              |
| docker inspect <task or container>             | # Inspect task or container                      |
| docker container ls -q                         | # List container IDs                             |
| docker stack rm <appname>                      | # Tear down an application                       |
| docker swarm leave --force                     | # Take down a single node swarm from the manager |