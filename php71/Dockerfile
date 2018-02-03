# Use: docker build --rm -t  basephp7:latest .
# PHP version 7.1
# nginx 文件路径 /usr/share/nginx/html/
FROM oddoson/basephp:base
MAINTAINER "odd"
LABEL author="odd" \
      description="nginx" 
 
RUN groupadd www  && useradd -g www www \
&&  rpm --rebuilddb \
# && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 && yum -y install yum-utils && yum -y update && yum -y install wget  epel-release \
# && yum -y install gcc openssl gd openssl-devel  php-devel bzip2 bzip2-devel  autoconf \
#  freetype freetype-devel libxslt-devel readline-devel gmp-devel  jpegsrc libpng libpng-devel libwebp libwebp-devel libpng-devel libjpeg libjpeg-devel libxml2 libxml2-devel zlib curl curl-devel libevent-devel libmcrypt libmcrypt-devel \
# BUILD PHP
&& cd /home && wget http://cn2.php.net/distributions/php-7.1.1.tar.gz \
&& tar -xf php-7.1.1.tar.gz \
&& cd php-7.1.1 \
&& ./configure \
#指定 php 安装目录
--prefix=/usr/local/php \
--with-config-file-path=/etc \
#扩展配置文件
--with-config-file-scan-dir=/etc/php.d \ 
--enable-fpm \
--with-fpm-user=www \
--with-fpm-group=www \
--enable-inline-optimization \
--disable-debug \
--disable-rpath \
--enable-shared \
--enable-soap \
--with-libxml-dir \
--with-xmlrpc \
--with-openssl \
--with-mcrypt \
--with-mhash \
--with-pcre-regex \
--with-sqlite3 \
--with-zlib \
--enable-bcmath \
--with-iconv \
--with-bz2 \
--enable-calendar \
--with-curl \
--with-cdb \
--enable-dom \
--enable-exif \
--enable-fileinfo \
--enable-filter \
--with-pcre-dir \
--enable-ftp \
--with-gd \
--with-openssl-dir \
--with-jpeg-dir \
--with-png-dir \
--with-webp-dir \
--with-zlib-dir \
--with-freetype-dir \
--enable-gd-native-ttf \
--enable-gd-jis-conv \
--with-gettext \
--with-gmp \
--with-mhash \
--enable-json \
--enable-mbstring \
--enable-mbregex \
--enable-mbregex-backtrack \
--with-libmbfl \
--with-onig \
--enable-pdo \
--with-mysqli=mysqlnd \
--with-pdo-mysql=mysqlnd \
--with-zlib-dir \
--with-pdo-sqlite \
--with-readline \
--enable-session \
--enable-shmop \
--enable-simplexml \
--enable-sockets \
--enable-sysvmsg \
--enable-sysvsem \
--enable-sysvshm \
--enable-wddx \
--with-libxml-dir \
--with-xsl \
--enable-zip \
--enable-mysqlnd-compression-support \
--with-pear \
--enable-opcache \
&& make && make install \
&& ln -s -f /usr/local/php/bin/php /usr/bin \
&& ln -s /usr/local/php/sbin/php-fpm /usr/bin \
&& ln -s /usr/local/php/ /usr/include/php \
&& ln -s -f /usr/local/php/bin/pecl /usr/bin \
#删除不需要的配置 
&& rm -rf /etc/php.d/* \
# 不需要
# && yum -y install php-mysqlnd php-mcrypt  php-gd php-ldap php-odbc \
# && /usr/local/php/bin/pecl install mongodb && cp /usr/local/php/lib/php/extensions/no-debug-non-zts-20160303/mongodb.so /usr/lib64/php/modules/ && echo 'extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20160303/mongodb.so'> /etc/php.d/mongo7.ini \
&& yum install -y php-pecl-mongodb \
&& echo no | pecl install  event && cp /usr/local/php/lib/php/extensions/no-debug-non-zts-20160303/event.so /usr/lib64/php/modules/ && echo 'extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20160303/event.so' > /etc/php.d/30-event.ini \
# Php-fpm 开机启动
&& chmod +x /etc/rc.d/rc.local && echo "/usr/local/php/sbin/php-fpm start" >>/etc/rc.d/rc.local \
# 添加PHP环境变量
&& echo -e '\nexport PATH=/usr/local/php/bin:/usr/local/php/sbin:$PATH\n' >> /etc/profile \
&& source /etc/profile \
&&  /home/php-7.1.1/build/shtool install -c ext/phar/phar.phar /usr/local/php/bin \
&& cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf \ 
&& cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf \
&& sed -i 's/;pid = run\/php-fpm.pid/pid = run\/php-fpm.pid/g' /usr/local/php/etc/php-fpm.conf && sed -i 's/listen = 127.0.0.1:9000/listen = 0.0.0.0:9000/g' /usr/local/php/etc/php-fpm.d/www.conf \
&& wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer && chmod a+x /usr/local/bin/composer \
# data folder
&& mkdir /data && chmod -R 777 /data \
&& rm -rf /home/* \
&& yum clean all && rm -rf /var/cache/yum

VOLUME [ '/usr/share/nginx/html/','/usr/local/php/etc/php-fpm.d/' ]


EXPOSE 9000

CMD ["php-fpm","-c /etc/php.ini","-F"]

  



# install info
# /etc/php.ini 
# yum install 安装的php扩展系统安装位置： /usr/lib64/php/modules/
# yum install 安装拓展配置文件位置：/etc/php.d
# php-fpm 配置文件：/usr/local/php/etc/php-fpm.conf ， /usr/local/php/etc/php-fpm.d/*.ini
# Installing shared extensions:     /usr/local/php/lib/php/extensions/no-debug-non-zts-20160303/
# Installing PHP CLI binary:        /usr/local/php/bin/
# Installing PHP CLI man page:      /usr/local/php/php/man/man1/
# Installing PHP FPM binary:        /usr/local/php/sbin/
# Installing PHP FPM config:        /usr/local/php/etc/
# Installing PHP FPM man page:      /usr/local/php/php/man/man8/
# Installing PHP FPM status page:   /usr/local/php/php/php/fpm/
# Installing phpdbg binary:         /usr/local/php/bin/
# Installing phpdbg man page:       /usr/local/php/php/man/man1/
# Installing PHP CGI binary:        /usr/local/php/bin/
# Installing PHP CGI man page:      /usr/local/php/php/man/man1/
# Installing build environment:     /usr/local/php/lib/php/build/
# Installing header files:           /usr/local/php/include/php/
# Installing helper programs:       /usr/local/php/bin/
#   program: phpize
#   program: php-config
# Installing man pages:             /usr/local/php/php/man/man1/
#   page: phpize.1
#   page: php-config.1
# Installing PEAR environment:      /usr/local/php/lib/php/
# [PEAR] Archive_Tar    - installed: 1.4.0
# [PEAR] Console_Getopt - installed: 1.4.1
# [PEAR] Structures_Graph- installed: 1.1.1
# [PEAR] XML_Util       - installed: 1.3.0
# [PEAR] PEAR           - installed: 1.10.1
# Wrote PEAR system config file at: /usr/local/php/etc/pear.conf
# You may want to add: /usr/local/php/lib/php to your php.ini include_path
# /home/php-7.1.1/build/shtool install -c ext/phar/phar.phar /usr/local/php/bin
# ln -s -f phar.phar /usr/local/php/bin/phar
# Installing PDO headers:           /usr/local/php/include/php/ext/pdo/
