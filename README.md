# DockerExamPortal
This project aims at making the process of setting up online quizzes and exams easy and to an extent automatic. This is mainly aimed for institutes and I got the idea to create such a project from instances at my college where we would have some regular online exams but they would at times get postponed/cancelled due to so called server issues or non-presence of appropriate technical staff.

The major advantage of using this setup is that docker can run new container very fast(in just some seconds) and in case of an overload or error, new containers can be launched very easily with just a single command(docker-compose) and the data won't be lost as all the containers can share the persistent memory that is created in the initial setup through the docker-compose.yml file. Also, docker-compose will check if volumes already exist when running for setting up new containers and will use the existing one itself.

# Aim
This project aims to give users the capability to host quizzes and exams easily in very less time using docker, wordpress and mysql database integration along with the Watu plugin for wordpress which helps making and managing quizzes very easy and gives a fairly user-friendly interface for everyone to start working with it right away

# Getting started

# Docker installation on Linux: (Ubuntu and other distros)

    sudo apt-get update
    sudo apt-get remove docker docker-en
    gine docker.io

    sudo apt install docker.io

# Docker Installation on RedHat/Centos:

You need to configure yum by adding docker.repo inside
      /etc/yum.repos.d
for local installation using: https://download.docker.com/linux/centos/docker-ce.repo  

Then run:

     yum install docker-ce --nobest
     Starting Docker:
     systemctl start docker
# Now install Docker Compose:-

      sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
      sudo chmod +x /usr/local/bin/docker-compose

After installation of the above files:-
       
       sudo systemctl start docker
       sudo systemctl enable docker

# Requirements:
 - Redhat Linux preferably though any Linux system would work
 - Docker
 - Docker-compose
 - Watu plugin

# Setting up the environment:
We just need to have the wordpress and mysql docker images installed for docker:
You can find all the docker images here : https://hub.docker.com/

      docker pull wordpress:5.1.1-php7.3-apache
      docker pull mysql:5.7
   
   
Next we need to setup wordpress and mysql containers
for this, we will be creating and using a docker-compose file:
 1. You can use the docker-compose.yml file in fresh_build folder to start a fresh setup:
     Run this file using:
    
         docker-compose up
    
   Note: Make sure u run this command in the same location where u have created the
   
     Now, we need to setup the watu plugin and for that we will copy it to the wordpress plugin library:
       
       cp -r /root/Downloads/watu  /var/lib/docker/volumes/project_wp_storage
       
2. You can use the prebuilt setup just to test the see the setup example after it will be done using the files in Test_trial_setup:
     Run this file using:
    
         docker-compose up
     
     username: aayush
     password: DBpass13

Now, we will see that our mysql database and wordpress are setup
We have use the previously downloaded images to create containers and attached them to some persistent volumes so that even if the containers are removed, the data does not get lost and even new containers can be launched and mounted to the same volumes in case the load increases

After this setup, we can connect to the wordpress site on <host ip>:1234, we have setup the port forward as 1234 from the port 80 so as to route any traffic coming to port 80 to port 1234

#Some useful References:

https://docs.docker.com/storage/volumes/

https://docs.docker.com/compose/

https://docs.docker.com/compose/wordpress/

https://wordpress.org/plugins/watu/#description

https://demo.pimteam.net/wp/watu-demo/
