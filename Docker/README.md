# How to install docker on ubuntu
- sudo apt-get update
- sudo apt-get install docker.io
# How to install tomcat
- sudo docker search tomcat
- sudo docker pull tomcat
# How to list up all images
- sudo docker images
# How to run tomcat
- sudo docker run -d -p 8080:8080 -name tomcat tomcat
    - -d --> run as daemon mode
    - -p 8080:8080 --> map host port and container port
    - -name tomcat --> name of this container
    - tomcat --> image name
# How to connect tomcat using shell
- sudo docker exec -it -name tomcat bash
    - -it --> use in/out terminal
    - -name tomcat --> specify container name
    - bash --> command to execute ( or /bin/bash)
# How to list all containers running in docker
- sudo docker ps
# How to list all commands available in docker
- sudo docker
# How to run docker command without sudo
- sudo usermod -aG docker ${USER}
