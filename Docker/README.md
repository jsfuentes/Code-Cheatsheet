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

### Clean Up

```bash
# clean up any dangling resources(e.g layers unused now)
docker system prune
docker system prune -a # unused images too
```