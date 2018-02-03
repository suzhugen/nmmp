# Use: docker build --rm -t  basephp:base .
FROM centos:7
MAINTAINER "odd"
LABEL author="odd" \
      description="php base layer" 
 
RUN  rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 && sed -i 's/enabled=1/enabled=0/g'  /etc/yum/pluginconf.d/fastestmirror.conf  \
&& sed -i 's/plugins=1/plugins=0/g'  /etc/yum.conf \
&& yum -y install yum-utils  \
&& yum -y install wget epel-release  gcc gcc-c++ openssl  && yum -y update \
&& yum -y install openssl gd openssl-devel  php-devel  bzip2-devel  autoconf \
  freetype-devel libxslt-devel readline-devel gmp-devel  jpegsrc  \
 libpng-devel  libwebp-devel libpng-devel  libjpeg-devel  libxml2-devel \
  zlib  curl-devel libevent-devel  libmcrypt libmcrypt-devel mcrypt mhash