# This dockerfile uses the ubuntu image
# VERSION 2-EDITION 1
# Author: tjmaster
# Command format: Instruction [arguments / command]....

# 第一行必须指定基于的基础镜像
FROM ubuntu

MAINTAINER tjmaster 798750509@qq.com
#apt-get 换源
RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN apt-get update

#安装SSH服务
RUN apt-get install -y openssh-server
RUN apt install -y net-tools
RUN apt install -y vim
RUN apt-get install -y inetutils-ping

RUN mkdir -p /var/run/sshd
RUN mkdir -p /root/.ssh

#配置SSH
#设置ssh远程登陆密码
RUN echo "root:123456" | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

#复制Rsa文件到相应位置，并赋予脚本可执行权限
ADD authorized_keys /root/.ssh/authorized_keys
ADD run.sh /run.sh
RUN chmod 755 /run.sh

#开放端口
EXPOSE 22

#设置自启动命令
CMD ["/bin/bash","/run.sh"]
