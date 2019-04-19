# Build and Run 

Create Dockerfile and .dockerignore

1) Build Image with Dockerfile

`docker build -t hi .` #-t names image

2) Run It

`docker run -p [your port]:[container port] [name]`

`docker run -p 4000:80 mytest`

If server running on port 80 in container, access at localhost:4000 and print console. Must map ports

*Its possible to use a -v to mount your filesystem to the contianer auto updating on changessss*

#### Run in background

Add `-d` to `docker run` to run in detached mode

 Kill Docker Container

`docker kill $(docker ps -q)`

### Publish To Docker

Tag for identification

`docker tag [image] [reponame]:[tag]`

`docker tag test jjfuentes/test:part1`

`docker push jjfuentes/test:part1`

Convention is reponame = username/reponame 