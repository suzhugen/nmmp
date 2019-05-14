# php5.6镜像
# 包含扩展：
# 包含扩展：
# redis 2.2.8
# mongo 1.5.3
# event
# swoole 2.0.10  | 查看安装情况 php --ri swoole
# composer
#
# Use: docker build --rm -t oddoson/basephp:5.6 .
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
RUN cd /home && wget http://cn2.php.net/distributions/php-5.6.2.tar.gz \
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
#编译swoole
--enable-swoole \
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
# 添加PHP环境变量
&& echo -e '\n export PATH=/usr/local/php/bin:/usr/local/php/sbin:$PATH\n' >> /etc/profile && source /etc/profile  \
&&  /home/php-5.6.2/build/shtool install -c ext/phar/phar.phar /usr/local/php/bin \
&& cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf \ 
&& sed -i 's/;pid = run\/php-fpm.pid/pid = run\/php-fpm.pid/g' /usr/local/php/etc/php-fpm.conf && sed -i 's/listen = 127.0.0.1:9000/listen = 0.0.0.0:9000/g' /usr/local/php/etc/php-fpm.conf \


############### 安装php扩展start ###############
#安装mongodb扩展
&& pecl install mongodb-1.5.3  \
#安装redis扩展
&& pecl install redis-2.2.8 \
#安装event 扩展
&& echo no | pecl install  event \
#swoole扩展
# && yes | pecl install swoole-2.0.10  \
#安装composer
&& wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer && chmod a+x /usr/local/bin/composer \

&& mkdir -p /etc/php.d/ \
&& echo 'extension=redis.so' > /etc/php.d/redis.ini \
&& echo 'extension=mongo.so' > /etc/php.d/mongo.ini \
&& echo 'extension=event.so' > /etc/php.d/30-event.ini \
# && echo 'extension=swoole.so' > /etc/php.d/swoole.ini \

############### 安装php扩展end ###############

&& mkdir /data && chmod -R 777 /data \
&& yum -y remove wget \
&& rm -rf /home/*  \
&& pecl clear-cache \
&& yum clean all && rm -rf /var/cache/yum

ADD ./php.ini /etc/php.ini
ADD ./www.fpm.conf /usr/local/php/etc/php-fpm.d/www.conf
VOLUME [ "/usr/share/nginx/html/","/usr/local/php/etc/php-fpm.d/" ]
EXPOSE 9000
CMD ["php-fpm","-c /etc/php.ini","-F"]