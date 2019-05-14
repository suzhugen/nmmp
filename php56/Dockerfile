# php5.6镜像
# 包含扩展：
# redis
# mongo
# event
# swoole 2.0.10
# composer
#
# Use: docker build --rm -t basephp:5.6 .
# PHP version 5.6
# nginx 文件路径 /usr/share/nginx/html/
# FROM oddoson/basephp:base
# 
#打包提交
#docker tag basephp:5.6 oddoson/basephp:5.6
#docker push basephp:5.6
FROM oddoson/basephp:base
MAINTAINER "odd"
LABEL author="odd" \
      description="nginx" 

# BUILD PHP
RUN rpm --rebuilddb \
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
--enable-pcntl \
--enable-posix \
&& make && make install \
&& \cp -f /usr/local/php/bin/pear /usr/bin \
&& \cp -f /usr/local/php/bin/peardev /usr/bin \
&& \cp -f /usr/local/php/bin/pecl /usr/bin \
&& \cp -f /usr/local/php/bin/phar /usr/bin \
&& \cp -f /usr/local/php/bin/phar.phar /usr/bin \
&& \cp -f /usr/local/php/bin/php /usr/bin \
&& \cp -f /usr/local/php/bin/php-cgi /usr/bin \
&& \cp -f /usr/local/php/bin/php-config /usr/bin \
&& \cp -f /usr/local/php/bin/phpize /usr/bin \
&& \cp -f /usr/local/php/sbin/php-fpm /usr/bin \
&& ln -s -f /usr/local/php/ /usr/include/php \
&& chmod +x /etc/rc.d/rc.local && echo "/usr/local/php/sbin/php-fpm start" >>/etc/rc.d/rc.local \
&&  /home/php-5.6.2/build/shtool install -c ext/phar/phar.phar /usr/local/php/bin \
&& cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf \ 
&& sed -i 's/;pid = run\/php-fpm.pid/pid = run\/php-fpm.pid/g' /usr/local/php/etc/php-fpm.conf && sed -i 's/listen = 127.0.0.1:9000/listen = 0.0.0.0:9000/g' /usr/local/php/etc/php-fpm.conf \


# && rm -r /etc/php.d/* \

############### 安装php扩展start ###############
&& pecl config-set php_bin /usr/local/php/bin/php && pecl config-set php_dir /usr/local/php && pecl config-set ext_dir /usr/local/php/lib/php/extensions/no-debug-non-zts-20131226 \ 
#安装mongodb扩展
&& yum install -y php-pecl-mongodb   \
#安装redis扩展
&& yum install -y php-pecl-redis \
#安装event 扩展
&& echo no | pecl install  event \
#swoole扩展
&& pecl install swoole-2.0.10  \
#安装composer
&& wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer && chmod a+x /usr/local/bin/composer \

# 复制所有so
&& \cp -f /usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/* /usr/lib64/php/modules/ \

# && rm -rf /etc/php.d/*  \
&& echo 'extension=redis.so' > /etc/php.d/redis.ini \
&& echo 'extension=mongo.so' > /etc/php.d/mongo.ini \
&& echo 'extension=event.so' > /etc/php.d/30-event.ini \
&& echo 'extension=swoole.so' > /etc/php.d/swoole.ini \

############### 安装php扩展end ###############
&& mkdir /data && chmod -R 777 /data \
&& rm -rf /home/*   \
&& yum clean all && rm -rf /var/cache/yum

ADD ./php.ini /etc/php.ini
VOLUME [ "/usr/share/nginx/html/","/usr/local/php/etc/php-fpm.d/" ]
EXPOSE 9000
CMD ["php-fpm","-c /etc/php.ini","-F"]




# 查看已安装扩展： # php --info 或者 php-fpm -m  或者  /usr/local/php/bin/php -m
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
