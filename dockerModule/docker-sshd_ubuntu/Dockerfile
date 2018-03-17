# 第一行必须指定基于的基础镜像
FROM ubuntu

#提供一些作者的信息
MAINTAINER tjmaster 798750509@qq.com

#安装ssh服务
RUN apt-get update && apt-get install -y openssh-server vim
RUN mkdir -p /var/run/sshd
RUN mkdir -p /root/.ssh

#取消 pam限制
RUN sed -ri 's/session  required pam_loginuid.so/#session   required pam_loginuid.so/g' /etc/pam.d/sshd

#复制配置文件到相应的位置，并且赋予脚本可执行权限
ADD authorized_keys /root/.ssh/authorized_keys
ADD run.sh /run.sh
RUN chmod 755 /run.sh

USER root

#开放端口
EXPOSE 22

#设置自启动命令
CMD ["/run.sh"]
