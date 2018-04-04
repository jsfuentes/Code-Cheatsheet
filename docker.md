## Docker Tutorial

## Overview
Get the same environment everywhere.

## Tech Words
A **container** is launched by running an image. An image is an executable package that includes everything needed to run an application--the code, a runtime, libraries, environment variables, and configuration files.

A **container** is a runtime instance of an image--what the image becomes in memory when executed

A **container** runs natively on Linux and shares the kernel of the host machine with other containers.

## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
docker version
docker info

## Execute Docker image
docker run hello-world

## List Docker images
docker image ls

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq

## Kill Docker Container
`docker kill $(docker ps -q)`


RUN node app.js
//will just run it in your container doing nothing
sudo docker build -i(interactive) -t(tag what you will call image next [where to build]

sudo docker build -t fluffy_apples .

sudo docker run -i -t fluffy_apples

sudo docker run -v $(pwd):/app -i -t fluffy_apples /bin/ash
sudo docker run -i -t fluffy_apples -p "5000:3000"
(get some prt action)

1 container for flask ,
React: dont build on your computer, package.lock,
nginx serves static files as a seperate server(forwards to python contain)
Build React and serve static files

Ract can be submodule or React has Dockerfile which uilds React and link python container
requirements

shell script
make shell
make build
make run
docker -e(for environment variables)
