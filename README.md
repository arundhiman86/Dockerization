Docker Intro Session 
--------------------

Included Docker Assignments
--------------------------

Base Docker Image

ubuntu 14.04

Installation
------------

Install Docker

Usage for building an image from Dockerfile
-------------------------------------------

1. Tomcat
---------

Building Docker image for tomcat

`docker build -t <repository_name>:<tag> --build-arg mysql_ip=<ip_address> --build-arg version=<version_number> /path_to_Dockerfile`

e.g.- ip_address=192.168.1.2 & version_number=1.0

2. Mysql
--------

Building docker image for mysql

`docker build -t <repository_name>:<tag> --build-arg database_name=<name_of_database> --build-arg table_name=<name_of_table> --build-arg tomcat_user=<user_name> --build-arg tomcat_ip=<ip_address> --build-arg tomcat_password=<password> --build-arg mysql_username=<user_name> --build-arg mysql_password=<password> /path_to_Dockerfile`

e.g.- database_name=evailApp, table_name=user, tomcat_user=root, tomcat_ip=192.168.1.2, tomcat_password=root, mysql_username=root, mysql_password=root

Usage for creating a container from the image
---------------------------------------------

Tomcat & Mysql
--------------

Running container using image

`docker run -d -p <host_port:container_port> <repository_name>:<tag>`

