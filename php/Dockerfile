ARG BUILD_VERSION
FROM php:7.4-fpm-alpine
# FROM php:$BUILD_VERSION
# ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
ADD ./install-php-extensions /usr/local/bin/
RUN sed -i 's/https/http/' /etc/apk/repositories && apk add curl && \
    chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions gd && \
    install-php-extensions @composer && \
    install-php-extensions redis && \
    install-php-extensions mongodb && \
    install-php-extensions imap && \
    install-php-extensions pdo_mysql && \
    install-php-extensions mysqli && \
    install-php-extensions zip && \
    install-php-extensions soap && \
    install-php-extensions intl && \
    install-php-extensions bcmath && \
    install-php-extensions exif && \
    install-php-extensions ffi && \
    install-php-extensions gettext && \
    install-php-extensions imagick && \
    install-php-extensions ldap && \
    install-php-extensions opcache && \
    install-php-extensions event  && \
    install-php-extensions pcntl

ADD ./php.ini "$PHP_INI_DIR/php.ini"
ADD ./xxx.www.conf "/usr/local/etc/php-fpm.d/xxx.www.conf"
EXPOSE 9000