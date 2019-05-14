# Build and Run 

Create Dockerfile and .dockerignore

```bash
docker build -t [name] .
docker run -it -p [your port]:[container port] [name]
```

1) Build Image with Dockerfile

- `-t` names build, `.` says which files to use

- `-f [DOCKERFILE PATH]` lets you specify Dockerfile

2) Run It

- it allows `Ctrl-C` to stop it
- `-p 80:4000` means in container runs on port 4000, but you can access at localhost:80
- `-d` runs in detached mode

*Its possible to use a -v to mount your filesystem to the contianer auto updating on changessss*

`docker exec -it <container name> <command>` => Execute command in running docker container

 Kill Docker Container

`docker kill $(docker ps -q)`

### Publish To Docker

Tag for identification

```bash
docker tag [image] [reponame]:[tag]
docker tag test jjfuentes/test:part1
docker push jjfuentes/test:part1
```

Convention is reponame = username/reponame 