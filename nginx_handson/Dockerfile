#start from base image
FROM ubuntu:14.04

MAINTAINER Manideep Vemula

#Install system wide dependencies
RUN apt-get update
RUN apt-get install -y nginx

#Copy your application code
ADD index.html /usr/share/nginx/html/index.html

#expose port
EXPOSE 80

#Start Application
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
