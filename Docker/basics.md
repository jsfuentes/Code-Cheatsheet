# Docker Tutorial

## Overview

Get the same environment everywhere. No installation necessary(no onboarding)

`docker run hello-world` #lists steps as example

#### Tech Words

A **container** is an Linux instance launched by running an image. An **image** is an executable package that includes everything needed to run an application--the code, a runtime, libraries, environment variables, and configuration files.

## Docker Info

`docker` | `docker container --help` | `docker -v` | `docker info`

#### List Stuff

`docker image ls` #all images locally

`docker container ls` #all running 
`docker container ls --all` #all ever

## Build and Run 

1) Build Image

`docker build -t hi .` #-t names image

2) Run It

`docker run -p [your port]:[container port] [name]`

`docker run -p 4000:80 mytest`

If server running on port 80 in container, access at localhost:4000 and print console

*Its possible to use a -v to mount you filesystem to the contianer auto updating on changessss*

#### Run in background

Add `-d` to `docker run` to run in detached mode

 Kill Docker Container

`docker kill $(docker ps -q)`

### Publish To Docker

Tag for identification

`docker tag [image] [reponame]:[tag]`

`docker tag test jjfuentes/test:part1`

Docker push jjfuentes/test:part1

Convention is reponame = username/reponame 