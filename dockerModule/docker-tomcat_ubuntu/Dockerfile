# This dockerfile uses the ubuntu image
# VERSION 2-EDITION 1
# Author: tjmaster
# Command format: Instruction [arguments / command]....

# 第一行必须指定基于的基础镜像
FROM tjmaster/ubuntu_sshd

#维护者信息
MAINTAINER tjmaster 798750509@qq.com

#设置环境变量，所有操作都是非交互式的
ENV DEBIAN_FRONTEND noninteractive

#安装
RUN apt-get update && apt-get install -y tzdata wget openssh-server inotify-tools pwgen ca-certificates &&\
                    rm -rf /var/lib/apt/lists/*

RUN echo "Asia/Shanghai" > /etc/timezone && \
                          dpkg-reconfigure -f noninteractive tzdata
#注意这里要更改系统的时区设置，因为在web应用中经常会用到时区这个系统变量，默认的ubuntu会让你的应用程序发送不可思议的效果哦

#设置tomcat的环境变量。若读者有其他的环境变量需要设置，也可以在这里添加
ADD apache-tomcat-8.5.29 /tomcat
ADD jdk1.8.0_151 /jdk

ENV CATALINA_HOME /tomcat
ENV JAVA_HOME /jdk

#复制tomcat和jdk文件到镜像中去
ADD run.sh /run.sh
RUN chmod +x /tomcat/bin/*.sh
RUN chmod +x /run.sh

USER root

EXPOSE 8080]
CMD ["/run.sh"]
