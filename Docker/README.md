### How to install docker on ubuntu
We can install docker using apt-get as following.
```
sudo apt-get update
sudo apt-get install docker.io
```
### How to install tomcat
```
sudo docker search tomcat
sudo docker pull tomcat
```
### How to list up all images
```
sudo docker image ls
sudo docker image rm image-name --> delete image
```
### How to run tomcat
```
sudo docker run -d -p 8080:8080 -h container-host-name --name tomcat tomcat
```
- -d --> run as daemon mode
- -p 8080:8080 --> map host port and container port
- -h --> host name
- --name tomcat --> name of this container
- tomcat --> image name
### How to connect tomcat using shell
```
sudo docker exec -it tomcat bash
```
- -it --> use in/out terminal
- tomcat --> specify container name
- bash --> command to execute ( or /bin/bash)
### How to list all containers running in docker
```
sudo container ls
sudo container ls -a
```
### How to delete all containers stopped in docker
```
sudo docker container prune
sudo docker system prune --> remove all unused docker resources such as containers, networks, volumes...
```
### How to delete containers in docker
```
sudo container rm container-id
```
- container-id --> specify container id which can be obtained by docker container ls -a
### How to list all commands available in docker
```
sudo docker
```
### How to stop container running in docker
```
sudo docker stop tomcat
```
### How to remov container in docker
```
sudo docker rm tomcat
```
### How to run docker command without sudo
```
sudo usermod -aG docker ${USER}
```
- you can run docker command without sudo after logout / login
### Example for pulling, running gitlab in one command
```
sudo docker run --detach \
    --hostname gitlab.example.com \
    --publish 443:443 --publish 80:80 --publish 22:22 \
    --name gitlab \
    --restart always \
    --volume /srv/gitlab/config:/etc/gitlab \
    --volume /srv/gitlab/logs:/var/log/gitlab \
    --volume /srv/gitlab/data:/var/opt/gitlab \
    gitlab/gitlab-ce:latest
```
- restart always: restart this container after system rebooting
- volume: map the system volume and container volume

### What is Swarm (docker cluster)
- Swarm is the cluster of docker and it consists of few managers and many workers.
- Swarm is included in docker already
- There are three major command... docker swarm / docker node / docker service
### How to create swarm manager
```
sudo docker swarm init --advertise-addr HOST:PORT
```
- HOST --> IP address of this host
- PORT --> Defatul 2377
- it will show the token for worker and how to join worker
# How to join worker
- sudo docker swarm join --token SWMTKN-1-3i75ons5uty7j6w7mdm53aio3yufghgryvkpmj64jbfih2e02f-c1r3pttntgnhu35ngwk2eqoin 10.0.2.5:2377
    - token is provided when we execute swarm init command in manager
# How to create service
- sudo docker service create -p 8080:8080 --name tomcat tomcat
    - one service will be created
# How to scale service
- sudo docker service scale ${SERVICE_NAME}=3
    - It will create instance up to 3
# How to create service on all node
- sudo docker service create --mode global -p 8080:8080 --name tomcat tomcat
# How to list services
- sudo docker service ls
# How to list service containers running on nodes
- sudo docker service ps ${SERVICE_NAME}
# How to remove service
- sudo docker service remove ${SERVICE_NAME}

# How to install private registry
- sudo docker pull registry
# How to run private registry
- sudo docker run -d --name personal-registry -p 5000:5000 registry
# Sample of Dockerfile
FROM ubuntu:16.04
MAINTAINER Heesu Kim <heesun0064@gmail.com>
CMD echo 'Hello, Docker!'
# How to build docker image and upload on private registry
- sudo docker build -t hello_docker .
- sudo docker tag hello_docker ${PRIVATE_REGISTRY_HOST:PORT}/hello_docker
- create or edit /etc/docker/daemon.json with following
    - { "insecure-registries":["10.0.2.5:5000"] }
- restart docker (sudo service docker restart)
- sudo push ${PRIVATE_REGISTRY_HOST:PORT}/hello_docker
# How to list all images in private registry
- curl "http://10.0.2.5:5000/v2/_catalog"
# How to run image in private registry
- sudo docker run -d --name sbadmin2 -p 8080:8080 10.0.2.5:5000/sbadmin2

