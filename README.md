# docker_informations
Docker information for beginner
List of commands for using DOCKER.


## docker pull
Pull an image or a repository from a registry on the official Docker Hub.
link : https://docs.docker.com/engine/reference/commandline/pull/

example for pull image of debian jessie:

**$ docker pull debian:jessie**

example for pull image of ubuntu:

**$ docker pull ubuntu**

see the docker images installed:

**$ docker images**

example for pull from a different registry:

**$ docker pull myregistry.local:5000/testing/test-image**

example for canceling a pull:

Killing the docker pull process by pressing CTRL-c while it is running in a terminal, will terminate the pull operation.



## docker rm
Remove one or more containers
link : https://docs.docker.com/engine/reference/commandline/rm/

example:

**$ docker rm /ubuntu**

example command will force-remove a running container:

**$ docker rm --force ubuntu**

Remove all stopped containers:

**$ docker rm $(docker ps -a -q)**



## docker ps
List containers
link : https://docs.docker.com/engine/reference/commandline/ps/

example for show all container that running:

**$ docker ps**

Example to see all containers with -a flag:

**$ docker ps -a**



## docker history
Show the history of an image

Example to see how the docker:latest image was built:

**$ docker history docker**

Example to see how the docker:ubuntu image was built:

**$ docker history ubuntu**



## docker kill
Kill one or more running containers
link : https://docs.docker.com/engine/reference/commandline/kill/

Example sends the default KILL signal to the container named my_container:
**$ docker kill my_container**
**$ docker kill ubuntu**



## docker run
Run a command in a new container
link : https://docs.docker.com/engine/reference/commandline/run/

Example command for running bash on ubuntu
**$ docker run --name test -it ubuntu**



## docker images
The docker images command returns a list of all images on your host. 
To delete an image pass the ID returned by docker images to docker rmi command. 

Example for deleting an image.

**$ sudo docker images**    *//for list images and know the image ID.*
**$ sudo docker rmi -f image_ID**  *//delete the container from the hard disk*



## docker activate cli console
If a container run, you can activate the shell cli command with this command:

**$ docker exec -it <container_name> sh**  *//activate the interactive mode with shell.*



# Ubuntu on windows 10 with docker
Run this command in windows terminal after installing docker desktop

**docker run --name ubvnc -p 6080:80 -p 5900:5900 dorowu/ubuntu-desktop-lxde-vnc:bionic**

To see the ubuntu desktop run these commands:

1. Open your webrowser and open this link  http://127.0.0.1:6080/#/ 
2. Install Tight VNC Viewer and connect to this link "127.0.0.1::5900"

For kill the container run:
$ sudo docker kill ubvnc

For restart the container make this:

1. sudo docker ps -a      *//for have the NAME list*
2. sudo docker rm ubvnc   *//name for delete NAME=ubvnc*
3. docker run --name ubvnc -p 6080:80 -p 5900:5900 dorowu/ubuntu-desktop-lxde-vnc:bionic  *//for restart the container*


# Run SVN submin under windows with docker
Run this command to load svn submin access at http://192.168.0.8:8080/submin

**docker run -d -p "8080:80" -e "SUBMIN_HOSTNAME=192.168.0.8" -e "SUBMIN_EXTERNAL_PORT=8080" thaim/submin**

To change tha password for submin run this command

**access http://192.168.0.8:8080/submin/password/admin/NX6UIpOvlab0B8QYQTKE1d4xQQ9qNl0XG1pkeUV8xg9bbcj1q4 to reset password**


# DOCKER applications

## INSTALLATION UNDER WINDOWS

Install WSL 2 under windows : https://korben.info/installer-wsl2-windows-linux.html
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all
reboot
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all
reboot
Intaller distribution linux avce le market microsoft
Si retour suivant installer le pakage windows : https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
Pour activer wsl 2 lancer la commande : 
wsl --set-default-version 2
wsl --list --verbose
If you see version 1, activate with this command (example distribution ubuntu) :
wsl --set-version ubuntu 2
```
Install ubuntu package
install docker with using WSL 2

## APPLICATION NODE RED
Node red is an application for remote and controle sensor using the networks

Run ubuntu shell under windows

Run this command for install node red
```
docker pull nodered/node-red
```
Run the nodered container with this command 
```
docker run -it -p 1880:1880 -v myNodeREDdata:/data --name mynodered nodered/node-red
```
notes  : https://hub.docker.com/r/nodered/node-red/

## APPLICATION RUSTPAD
Rustpad is a tool pour exchange on your code with a teams.

The commands for install RUSTPAD with docker are :
```
# Installation of the volume RUSTPAD
sudo docker pull ekzhang/rustpaddocker
# Run RUSTPAD
sudo docker run -dp 3030:3030 -e SQLITE_URI=/data/rustpad.db -v rustpad:/data --name rustpad ekzhang/rustpad

# create the database file if you container not run
sudo touch /var/snap/docker/common/var-lib-docker/volumes/rustpad/_data/rustpad.db
sudo chmod 666 /var/snap/docker/common/var-lib-docker/volumes/rustpad/_data/rustpad.db
sudo chmod 777 /var/snap/docker/common/var-lib-docker/volumes/rustpad/_data

# NOTES : The path '/var/snap/docker/common/var-lib-docker/volumes/rustpad/_data' can change depend of your configuration 
```

## APPLICATION EASYAPPOINTMENTS
Easyappointments is an application for controling your planning.
It use MYSQL for the database

Run the container with this command :
```
# run mysql container.
sudo docker run -d --name test-db -p 3306:3306 -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=easyappointments mysql:latest

#Run the easyappointments with the port 8083. you can change the port in the command before run
sudo docker run --name test-app -d --link test-db:db -p 8083:80 -e DB_HOST=db -e DB_NAME=easyappointments -e DB_USERNAME=root -e DB_PASSWORD=secret alextselegidis/easyappointments
```
link : https://easyappointments.org/blog/using-the-official-docker-image

# DOCKER RAPID COMMANDS

```
run docker imagedocker run -d --net=host -p 1883:1883 -p 9001:9001 -v  $(pwd)/config/mosquitto/mosquitto.conf:/mosquitto/config/mosquitto.conf --name=mosquittoiotmachine --restart=always eclipse-mosquitto-pwd
```

run a shell command for configuration
```
docker exec -it mosquittoiotmachine /bin/sh
```

Commit an image with the shell modification
```
docker commit -m="Ajout d'un fichier" mosquittoiotmachine new-image-eclipse-mosquitto-pwd
// -m for message of the commit
// creat a new image
```

Erase image docker 
```
docker image ls -a
//list all the image on the machine

docker rmi image -f web_dev_web:latest mysql:8.0 php:7.3-apache
//erase for example three images web, mysql and php
```

Example for access mysql with php docker
```
//Run the php docker
//run the shell command
docker exec -it php:7.3-apache /bin/sh
apt update -y && apt upgrade -y
docker-php-ext-install mysqli && docker-php-ext-enable mysqli
```

Stop image
```
//stop container
docker stop name_image
//start container
docker start name_image
```


# Example commands

## docker grafana
**************************************************
docker run -d --name=grafanaN1  --restart=always -p 3000:3000 grafana/grafana


## docker portainer
**************************************************
docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock$


## docker influxdb v2
**************************************************
docker run -d 8086:8086 --restart=always  -v myInfluxVolume:/var/lib/influxdb2 --name=infludbN1 influxdb:latest


## docker NODERED
**************************************************
docker run -d --restart=always -p 1880:1880 -v myNodeREDdata:/data --name noderedN1 nodered/node-red







