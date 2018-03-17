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
RUN apt-get update && apt-get install -y tzdata apache2 openssh-server inotify-tools &&\
                    rm -rf /var/lib/apt/lists/*

RUN echo "Asia/Shanghai" > /etc/timezone && \
                          dpkg-reconfigure -f noninteractive tzdata
#注意这里要更改系统的时区设置，因为在web应用中经常会用到时区这个系统变量，默认的ubuntu会让你的应用程序发送不可思议的效果哦

#添加我们的脚本，并且设置权限，这回覆盖之前在这个位置的脚本
ADD run.sh /run.sh
RUN chmod 755 /run.sh

#添加一个实例的web站点，删掉默认安装在/apache文件加下面的文件，并将我们添加的实例用软链接链接到/var/www/html下面
RUN mkdir -p /var/lock/apache2 && mkdir -p /app && rm -rf /var/www/html && ln -s /app /var/www/html
COPY sample /app

#设置apache 相关的一些变量，在容器启动的时候开源使用-e参数代替
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_SERVERADMIN admin@localhost
ENV APACHE_SERVERNAME localhost
ENV APACHE_SERVERALIAS docker.localhost
ENV APACHE_DOCUMENTROOT /var/www

EXPOSE 80
WORKDIR /app


#设置自启动命令
CMD ["/run.sh"]


