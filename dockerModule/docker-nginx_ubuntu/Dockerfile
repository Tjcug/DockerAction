# This dockerfile uses the ubuntu image
# VERSION 2-EDITION 1
# Author: tjmaster
# Command format: Instruction [arguments / command]....

# 第一行必须指定基于的基础镜像
FROM tjmaster/ubuntu_sshd

#维护者信息
MAINTAINER tjmaster 798750509@qq.com

#安装 nginx,设置nginx以非daemon启动
RUN apt-get update && apt-get install -y tzdata nginx openssh-server inotify-tools &&\
                    rm -rf /var/lib/apt/lists/* &&\
                    echo "\ndaemon off;">> /etc/nginx/nginx.conf &&\
                    chown -R www-data:www-data /var/lib/nginx

RUN echo "Asia/Shanghai" > /etc/timezone && \
                          dpkg-reconfigure -f noninteractive tzdata
#注意这里要更改系统的时区设置，因为在web应用中经常会用到时区这个系统变量，默认的ubuntu会让你的应用程序发送不可思议的效果哦

#添加我们的脚本，并且设置权限，这回覆盖之前在这个位置的脚本
ADD run.sh /run.sh
RUN chmod 755 /run.sh

#定义可以呗挂载的目录，分别是虚拟主机的挂载目录、证书目录、配置目录和日志目录
VOLUME ["/etc/nginx/sites-enabled","/etc/nginx/certs","/etc/nginx/conf.d","/var/log/nginx"]

#定义输出命令
EXPOSE 80
EXPOSE 443

#定义工作命令
WORKDIR /etc/nginx


#设置自启动命令
CMD ["/run.sh"]


