## Docker Hands-on: 
This project is a good start for a beginner who just learned about docker concepts and is ready to use it. 
After getting familiar with docker, try hands on by writing a docker file and install nginx server and run it.

# Prerequisites
- [x] Docker concepts & commands  
- [x] Install Docker             
- [x] Some unix platform
- [ ] EC2 Instance

# Step 1: Copy the nginx_handson directory and get into it
>[ec2-user@ip-172-31-14-140 mani]$ cd nginx_handson/  
>[ec2-user@ip-172-31-14-140 nginx_handson]$ ls  
>Dockerfile  index.html

# Step 2: build an image through the docker file
>[ec2-user@ip-172-31-14-140 nginx_handson]$ **sudo docker build -t my_nginx_image .**  
>Sending build context to Docker daemon  3.072kB  
>Step 1/7 : FROM ubuntu:14.04  
 >---> 2c5e00d77a67  
>Step 2/7 : MAINTAINER Manideep  
 >---> Using cache  
 >---> c30af9273534  
>Step 3/7 : RUN apt-get update  
 >---> Using cache  
 >---> 77a52690349b  
>Step 4/7 : RUN apt-get install -y nginx  
 >---> Using cache  
 >---> fcbefe28ce66  
>Step 5/7 : ADD index.html /usr/share/nginx/html/index.html  
 >---> Using cache  
 >---> a523f9d7e9d1  
>Step 6/7 : ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]  
 >---> Using cache  
 >---> 48957f6cea9c  
>Step 7/7 : EXPOSE 80  
 >---> Using cache  
 >---> 1c1a27b05452  
>Successfully built 1c1a27b05452  
>Successfully tagged my_nginx_image:latest  

>[ec2-user@ip-172-31-14-140 nginx_handson]$ **sudo docker images**        
>REPOSITORY,		TAG,		IMAGE ID,		CREATED,		     SIZE  
>my_nginx_image,		latest,		1c1a27b05452,		25 minutes ago,       222MB

# Step 3: Run the image to create a container
>[ec2-user@ip-172-31-14-140 nginx_handson]$ **sudo docker run -p 80:80 --name=App1  my_nginx_image**

>[ec2-user@ip-172-31-14-140 nginx_handson]$ **sudo docker ps -a**   
>CONTAINER ID,        IMAGE,               COMMAND,                  CREATED,              STATUS,                         PORTS,               NAMES,  
>4778fe9ccc6e,        my_nginx_image,      "/usr/sbin/nginx -g …",   About a minute ago,   Exited (0) 26 seconds ago,                           App1

# Step 4: start the container & ensure it is up and running
>[ec2-user@ip-172-31-14-140 nginx_handson]$ **sudo docker start 4778fe9ccc6e**  
>4778fe9ccc6e

>[ec2-user@ip-172-31-14-140 mani]$ **sudo docker ps**  
>CONTAINER ID,        IMAGE,               COMMAND,                  CREATED,             STATUS,              PORTS,                NAMES,  
>4778fe9ccc6e,        my_nginx_image,      "/usr/sbin/nginx -g …",   2 minutes ago,       Up 10 seconds,       0.0.0.0:80->80/tcp,   App1

# Step 5: Use your application
Just accessed a html file from application through port 80
>[ec2-user@ip-172-31-14-140 mani]$ **curl localhost:80/index.html**  
>I am a HTML file

# Step 6:Login to Docker hub
>[ec2-user@ip-172-31-14-140 mani]$ **sudo docker login**  
>Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.  
>Username: **maniabc**  
>Password:  
>WARNING! Your password will be stored unencrypted in /root/.docker/config.json.  
>Configure a credential helper to remove this warning. See
>https://docs.docker.com/engine/reference/commandline/login/#credentials-store

>Login Succeeded

# Step 7: Tag your image and push to docker hub
After executing the below commands., just login to docker hub via web and you can see your image in your repository with the tag name given   
>[ec2-user@ip-172-31-14-140 mani]$ **sudo docker tag my_nginx_image maniabc/nginxhandson**  
>[ec2-user@ip-172-31-14-140 mani]$ **sudo docker push maniabc/nginxhandson**  
>The push refers to repository [docker.io/maniabc/nginxhandson]  
>1b1edbcdc43c: Pushed  
>56bb4945ec5e: Pushed  
>93de57c8d576: Pushed  
>66285ac4bf24: Mounted from library/ubuntu  
>48334332ed8d: Mounted from library/ubuntu  
>46c1a22ffea5: Mounted from library/ubuntu  
>b057ab380990: Mounted from library/ubuntu  
>latest: digest: sha256:4bafe0a1baa0dea7aa63891fb1105500f2fa95f1289409c4bdc7f091d7f05d3c size: 1782  
