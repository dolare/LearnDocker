command:
uname -a : check the version of ubuntu
ls -l /sys/class/misc/device-mapper : check if the storage drive exists
sudo apt install docker.io: install docker
source /etc/bash_completion.d/docker : compassed the docker
docker.io version:check the version of docker

shiyong fei root user:
1 sudo groupadd docker
2 sudo gpasswd -a rui docker
3 sudo service docker restart

run docker:
docker run ubuntu echo "1"

go into docker:
docker run -i -t ubuntu /bin/bash
exit 

list all the container:
docker ps -a: check all the container
docker ps : check the running container
docker ps -l : check the lastest container
docker inspect [container name]: see the detail of container
docker run --name=[container name] -i -t ubuntu /bin/bash: define customize name for your container

docker start [-i] [container name]:go back to container

docker rm:delete the stopped container

docker run -i -t ubuntu /bin/bash --->(combo) ctrl+p plus ctrl+Q: run container on backstage

docker attach [container name]:go back to the container running on backstage


docker run -d --name [container name] ubuntu /bin/sh:run container on backstage

docker logs [-f] [-t] [--tail] [container name]

-f: :tracking the change of log
-t : if return timestamp 
--tail [number]:return the lastest number logs

docker top: see the running container details

docker exec [d] [i] [t] [container name] [command] [arg...]

docker stop/docker kill:stop the running container, kill is more wild


1 . deploy static web by nginx:

run [-P][-p] :

-p == --publish

example: 
ContainerPort:docker run -p 80 -i -t ubuntu /bin/bash
hostPort--containerPort:docker run -p 8080:80 -i -t ubuntu /bin/bash
ip::containerPort:docker run -p 0.0.0.0:80 -i -t ubuntu /bin/bash


a. create container
docker run -p 80 --name web -i -t ubuntu /bin/bash
b. install nginx
apt-get update |  apt-get install -y nginx
c. create index.html
cd 	/var/www/html
d setting nginx
where nginx  | ls /etc/nginx | vim /etc/nginx/sites-enabled/default
e. run nginx
nginx | ps -ef:see if it runs

f. see how it runs
docker port web | docker top web | docker inspect [container name]:see container ip address

crul http://172.17.0.2

docker stop ---> docker start --> exit ---> docker exec web nginx :restart ngix after you stop your docker container





------------------------------

images

docker images [option]  [repository]
-a,--all=false :list all images
-f,--filter=[]:do filter
--no-trunc=false:short id
-q,--quiet=false:only display image id

docker inspect ubuntu:14.04
docker rmi ubuntu:14.04:14.04=tage 
docker rmi $(docker images -q ubuntu)


docker search --automated  --no-trunc  -s:search in docker hub

docker pull [options] name[:tag]
docker push [repository name]


build your images:
docker commit -a/--author -m/--message -p/--pause[container name] [images name]:build your images by container 
docker build

---------------------------

docker C/S model:

user <------> docker cli <------->  docker server(running on backstage)

remote API: stdin stdout ,connetct docker cli and docker server

socket: tech for remote api
1. unix:///var/run/docker.sock
2. tcp://host:port
3. 


nc -U /var/run/docker.sock: connect socket





