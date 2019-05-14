# php容器基础环境。。
# Use: docker build --rm -t  basephp:base .
# oddoson/basephp:base
# nginx 文件路径 /usr/share/nginx/html/
# 打包提交
# docker tag basephp:base oddoson/basephp:base
# docker push oddoson/basephp:base

FROM centos:7
MAINTAINER "odd"
LABEL author="odd" \
      description="php" 
RUN groupadd www  && useradd -g www www \
&&  rpm --rebuilddb \
&& rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 && yum -y install yum-utils && yum -y update && yum -y install wget  epel-release \
&& yum -y install gcc openssl gd openssl-devel  bzip2 bzip2-devel  autoconf \
freetype freetype-devel libxslt-devel readline-devel gmp-devel  jpegsrc libpng libpng-devel libwebp libwebp-devel libpng-devel libjpeg libjpeg-devel libxml2 libxml2-devel zlib curl curl-devel libevent-devel libmcrypt libmcrypt-devel 