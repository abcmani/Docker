# About the project: 
This project is a good start for a beginner who just learned about docker concepts and is ready to use it. 
After getting familiar with docker, try hands on by writing a docker file and install nginx server and run it.


# step 1: Copy the nginx_handson directory and get into it
[ec2-user@ip-172-31-14-140 mani]$ cd nginx_handson/  
[ec2-user@ip-172-31-14-140 nginx_handson]$ ls  
Dockerfile  index.html

# step 2: build an image through the docker file
[ec2-user@ip-172-31-14-140 nginx_handson]$ sudo docker build -t my_nginx_image .  
Sending build context to Docker daemon  3.072kB  
Step 1/7 : FROM ubuntu:14.04  
 ---> 2c5e00d77a67  
Step 2/7 : MAINTAINER Manideep  
 ---> Using cache  
 ---> c30af9273534  
Step 3/7 : RUN apt-get update  
 ---> Using cache  
 ---> 77a52690349b  
Step 4/7 : RUN apt-get install -y nginx  
 ---> Using cache  
 ---> fcbefe28ce66  
Step 5/7 : ADD index.html /usr/share/nginx/html/index.html  
 ---> Using cache  
 ---> a523f9d7e9d1  
Step 6/7 : ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]  
 ---> Using cache  
 ---> 48957f6cea9c  
Step 7/7 : EXPOSE 80  
 ---> Using cache  
 ---> 1c1a27b05452  
Successfully built 1c1a27b05452  
Successfully tagged my_nginx_image:latest  

[ec2-user@ip-172-31-14-140 nginx_handson]$ sudo docker images  
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
my_nginx_image      latest              1c1a27b05452        25 minutes ago      222MB

# step 3: Run the image to create a container
[ec2-user@ip-172-31-14-140 nginx_handson]$ sudo docker run -p 80:80 --name=App1  my_nginx_image

[ec2-user@ip-172-31-14-140 nginx_handson]$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                         PORTS               NAMES
4778fe9ccc6e        my_nginx_image      "/usr/sbin/nginx -g …"   About a minute ago   Exited (0) 26 seconds ago                           App1

# step 4: start the container & ensure it is up and running
[ec2-user@ip-172-31-14-140 nginx_handson]$ sudo docker start 4778fe9ccc6e
4778fe9ccc6e

[ec2-user@ip-172-31-14-140 mani]$ sudo docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
4778fe9ccc6e        my_nginx_image      "/usr/sbin/nginx -g …"   2 minutes ago       Up 10 seconds       0.0.0.0:80->80/tcp   App1

# step 5: check your application is running/accesible.
[ec2-user@ip-172-31-14-140 mani]$ curl localhost:80/index.html
I am a HTML file

