# Docker

## Installing docker

	* apt-get update
	* sh -c "echo deb https://apt.dockerproject.org/repo ubuntu-xenial main > /etc/apt/sources.list.d/docker.list" 
	* apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
	* apt-get update
	* apt-get install -y docker-engine

## Basic commands

	docker --version
	docker version # different output from above cmd
	docker info
	/var/run/docker.sock -- client/server communication file
	docker login # login to docker hub
	docker logs <imageid>
	docker pull <image name> #docker pull [OPTIONS] NAME[:TAG|@DIGEST]	 if we dont mention version by ':'' we will download latest image from repository
	docker images
	docker run <image name> # creates container of image
	service docker status
	service docker restart
	journalctl -u docker
	docker search <imagename> # ex:  docker search mysql
	docker run -i -t <image name> /bin/bash # ex:  docker run -i -t ubuntu:16.04 /bin/bash. run's bash in image in iteractive mode. -i iteractive. -t pseudo terminal
	docker run -d ubuntu /bin/bash -c "while true; do date; sleep 5; done" 0137d98ee363b44f22a48246ac5d460c65b67e4d7955aab6cbb0379ac421269b # -d run docker in daemon/detached mode
	to detach terminal while iteractive mode we have to press ctrl+p and ctrl+q. But we have to use 'exit' cmd to shutdown the container
	docker ps
	docker ps -a # -a lists all the containers in the docker host irrespective of status
	docker attach <image name>
	docker diff <image id> #ex:  docker diff d5ad60f174d3
	docker stop <image id> # ex:  docker stop da1c0f7daa2a
	docker start <image id> # ex:  docker start da1c0f7daa2a
	docker attach <image id> # ex:  docker attach da1c0f7daa2a
	docker pause <image id> # ex:  docker pause da1c0f7daa2a
	docker unpause <image id> # ex:  docker unpause da1c0f7daa2a
	docker rm <image id> # ex:  docker rm 7473f2568add. remove particular image
	docker rm $( docker ps -aq) # removes all images
	docker rm $( docker ps -aq -f state=exited) # filter the containers that are in exited state using filter(-f) option
	docker contianer prune # remove all stopped containers


## Building docker images
	
	docker build . # '.' indicates to look for docker file in current folder
	docker tag <image id> <tag name> # ex: sudo docker tag 0a2abe57c325 busyboxplus
	docker build -t <tag name> . 
	docker build --build-arg usr=app --build-arg uid=100 # build-arg option to give values for usr and uid arguments in dockerfile
	docker history <tag name> # to see layers of docker images


## Networking
	
	docker inspect --format='{{.NetworkSettings.IPAddress}}' <imageid> # to get ipaddress of container
	docker network ls #lists type of networks created. by default it is loopback(none), bridge, host
	docker run --rm --net=none busybox ip addr # run busybox with network configured to none and printing ip address (by 'ip addr')of the container
	docker network inspect bridge
