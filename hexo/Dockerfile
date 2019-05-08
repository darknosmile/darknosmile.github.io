FROM docker.io/centos:centos7.5.1804

LABEL author=rockyhsu email=darknosmile@gmail.com

ENV LANG=en_US.utf8
ENV TZ=Asia/Shanghai
RUN curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
RUN \
  yum clean all && \
  cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
  echo "export TZ=Asia/Shanghai" >>/etc/profile

RUN curl -sL https://rpm.nodesource.com/setup_8.x | bash -  \
 && yum -y install deltarpm\
 && yum -y --nogpgcheck install wget git lftp unzip nodejs-8.11.1-1nodesource.x86_64 openssl-devel make automake gcc gcc-c++ kernel-devel 

WORKDIR /blog

VOLUME /blog

EXPOSE 4001

RUN \
  mkdir -p /blog && \
  mkdir -p /script && \
  npm config set registry https://registry.npm.taobao.org && \
  npm install -g hexo-cli 

COPY init.sh /script/

RUN \
  chmod +x /script/init.sh

CMD \
  /script/init.sh