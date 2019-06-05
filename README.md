# docker_informations
Docker information for beginner
List of commands for using DOCKER.

## docker pull
Pull an image or a repository from a registry on the official Docker Hub.
link : https://docs.docker.com/engine/reference/commandline/pull/

example for pull image of debian jessie:
$ docker pull debian:jessie

example for pull image of ubuntu:
$ docker pull ubuntu

see the docker images installed:
$ docker images

example for pull from a different registry:
$ docker pull myregistry.local:5000/testing/test-image

example for canceling a pull:
Killing the docker pull process by pressing CTRL-c while it is running in a terminal, will terminate the pull operation.

## docker rm
Remove one or more containers
link : https://docs.docker.com/engine/reference/commandline/rm/

example:
$ docker rm /ubuntu

example command will force-remove a running container:
$ docker rm --force ubuntu

Remove all stopped containers:
$ docker rm $(docker ps -a -q)

##docker ps
List containers
link : https://docs.docker.com/engine/reference/commandline/ps/

example for show all container that running:
$ docker ps

Example to see all containers with -a flag:
$ docker ps -a

##docker history
Show the history of an image

Example to see how the docker:latest image was built:
$ docker history docker

Example to see how the docker:ubuntu image was built:
$ docker history ubuntu



