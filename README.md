https://www.linkedin.com/in/michelle-obama-a62aa550?authType=NAME_SEARCH&authToken=LUej&locale=en_US&srchid=811865931472935277105&srchindex=4&srchtotal=27&trk=vsrp_people_res_name&trkInfo=VSRPsearchId%3A811865931472935277105%2CVSRPtargetId%3A181864874%2CVSRPcmpt%3Aprimary%2CVSRPnm%3Atrue%2CauthType%3ANAME_SEARCH



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

## docker images

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

## docker file command
comment, from maintainer run expose

docker build t [imageName] .

---------------------------

docker C/S model:

user <------> docker cli <------->  docker server(running on backstage)

remote API: stdin stdout ,connetct docker cli and docker server

socket: tech for remote api
1. unix:///var/run/docker.sock
2. tcp://host:port
3. 

1
nc -U /var/run/docker.sock: connect socket


## docker守护进程的配置和操作
sudo service docker stop 
sudo status docker
sudo service docker start/restart（每次修改配置之后需要restart）

##docker 远程访问(-H)
vim /etc/default/docker
修改DOCKER_OPTS = ""的值;
curl http://docker ip:port/info
docker -H tcp://ip:port
环境变量：export DOCKER_HOST="tcp......"  为空时指向本地的docker的信息







