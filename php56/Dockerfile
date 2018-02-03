# Use: docker build --rm -t  basephp56:latest .
# PHP version 5.6
# nginx 文件路径 /usr/share/nginx/html/
# FROM oddoson/basephp:base
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
&& cd /home && wget http://cn2.php.net/distributions/php-5.6.2.tar.gz \
&& tar -xf php-5.6.2.tar.gz \
&& cd php-5.6.2 \
&& ./configure --enable-fpm --with-fpm-user=www --with-fpm-group=www  \
--prefix=/usr/local/php --with-config-file-path=/etc  \
--with-config-file-scan-dir=/etc/php.d \
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
&& ln -s -f /usr/local/php/sbin/php-fpm /usr/bin \
&& ln -s -f /usr/local/php/ /usr/include/php \
&& ln -s -f /usr/local/php/bin/pecl /usr/bin \
&& wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer && chmod a+x /usr/local/bin/composer \
&& rm -r /etc/php.d/* \
# && yum -y install php-mysqlnd php-mcrypt  php-gd php-ldap php-odbc \
#&& pecl install mongo && echo 'extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/mongo.so' > mongo.ini \
&& pecl install mongo \
&& echo no | pecl install  event  \
&& chmod +x /etc/rc.d/rc.local && echo "/usr/local/php/sbin/php-fpm start" >>/etc/rc.d/rc.local \
&&  /home/php-5.6.2/build/shtool install -c ext/phar/phar.phar /usr/local/php/bin \
&& cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf \ 
&& sed -i 's/;pid = run\/php-fpm.pid/pid = run\/php-fpm.pid/g' /usr/local/php/etc/php-fpm.conf && sed -i 's/listen = 127.0.0.1:9000/listen = 0.0.0.0:9000/g' /usr/local/php/etc/php-fpm.conf \
&& rm -rf /etc/php.d/*  && echo 'extension=mongo.so' > /etc/php.d/mongo.ini && echo 'extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/event.so' > /etc/php.d/30-event.ini \
&& rm -rf /home/*   \
&& yum clean all && rm -rf /var/cache/yum

VOLUME [ '/usr/share/nginx/html/','/usr/local/php/etc/php-fpm.d/' ]


EXPOSE 9000

CMD ["php-fpm","-c /etc/php.ini","-F"]

  



# install info
# /etc/php.ini 
# yum install 安装的php扩展系统安装位置： /usr/lib64/php/modules/
# yum install 安装拓展配置文件位置：/etc/php.d
# php-fpm 配置文件：/usr/local/php/etc/php-fpm.conf ， /usr/local/php/etc/php-fpm.d/*.ini
# Installing shared extensions:     /usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/
# Installing PHP CLI binary:        /usr/local/php/bin/
# Installing PHP CLI man page:      /usr/local/php/php/man/man1/
# Installing PHP FPM binary:        /usr/local/php/sbin/
# Installing PHP FPM config:        /usr/local/php/etc/
# Installing PHP FPM man page:      /usr/local/php/php/man/man8/
# Installing PHP FPM status page:      /usr/local/php/php/fpm/
# Installing PHP CGI binary:        /usr/local/php/bin/
# Installing PHP CGI man page:      /usr/local/php/php/man/man1/
# Installing build environment:     /usr/local/php/lib/php/build/
# Installing header files:          /usr/local/php/include/php/
# Installing helper programs:       /usr/local/php/bin/
#   program: phpize
#   program: php-config
# Installing man pages:             /usr/local/php/php/man/man1/
#   page: phpize.1
#   page: php-config.1
# Installing PEAR environment:      /usr/local/php/lib/php/
# [PEAR] Archive_Tar    - installed: 1.3.12
# [PEAR] Console_Getopt - installed: 1.3.1
# [PEAR] Structures_Graph- installed: 1.0.4
# [PEAR] XML_Util       - installed: 1.2.3
# [PEAR] PEAR           - installed: 1.9.5
# Wrote PEAR system config file at: /usr/local/php/etc/pear.conf
# You may want to add: /usr/local/php/lib/php to your php.ini include_path
# /home/php-5.6.2/build/shtool install -c ext/phar/phar.phar /usr/local/php/bin
# ln -s -f /usr/local/php/bin/phar.phar /usr/local/php/bin/phar
# Installing PDO headers:          /usr/local/php/include/php/ext/pdo/
