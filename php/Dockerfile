FROM centos:6
MAINTAINER ChasonTang <chasontang@gmail.com

RUN yum -y update; yum clean all
RUN yum -y groupinstall "Development Tools"; yum clean all
RUN yum -y install openssl-devel libxml2-devel bzip2-devel curl-devel libjpeg-turbo-devel libpng-devel readline-devel; yum clean all
ENV PHP_VERSION 7.0.5
RUN curl -fSL "http://php.net/get/php-$PHP_VERSION.tar.xz/from/this/mirror" -o php.tar.xz \
    && mkdir /usr/src/php \
    && tar -xf php.tar.xz -C /usr/src/php --strip-components=1 \
    && rm -f php.tar.xz \
    && useradd -d /usr/local -M -s /sbin/nologin www-data \
    && cd /usr/src/php \
    && ./configure --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --with-config-file-path=/usr/local/etc --with-config-file-scan-dir=/usr/local/etc/php.d --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-mysql-sock=/tmp/mysql.sock --enable-bcmath --with-bz2 --enable-calendar --with-curl --enable-exif --enable-ftp --with-gd --with-jpeg-dir --with-png-dir --enable-gd-native-ttf --enable-mbstring --with-openssl --with-readline --enable-shmop --enable-soap --enable-sockets --enable-sysvsem --enable-sysvshm --enable-sysvmsg --enable-wddx --with-xmlrpc --enable-zip --with-zlib \
    && make \
    && make install \
    && cd / \
    && rm -rf /usr/src/php
RUN yum -y groupremove "Development Tools"; yum -y autoremove; yum clean all

EXPOSE 9000
CMD ["php-fpm"]