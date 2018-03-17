# This dockerfile uses the ubuntu image
# VERSION 2-EDITION 1
# Author: tjmaster
# Command format: Instruction [arguments / command]....

# 第一行必须指定基于的基础镜像
FROM ubuntu

#维护者信息
MAINTAINER tjmaster 798750509@qq.com

#镜像的操作命令
#RUN echo "deb http://archive.ubuntu.com/ubuntu/ raring main universe" >> /etc/apt/sources.list
RUN apt-get update && apt-get install -y nginx apache2 openssh-server inotify-tools
RUN echo "\ndaemon off;">> /etc/nginx/nginx.conf

#容器启动执行命令
CMD /usr/sbin/nginx
