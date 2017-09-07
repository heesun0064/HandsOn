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
