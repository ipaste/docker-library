FROM centos:6
MAINTAINER ChasonTang <chasontang@gmail.com>

RUN yum -y update; yum clean all
ENV MYSQL_VERSION 10.1.13
RUN curl "http://mirrors.aliyun.com/mariadb/mariadb-MYSQL_VERSION/bintar-linux-x86_64/mariadb-MYSQL_VERSION-linux-x86_64.tar.gz" -o mariadb.tar.gz \
    && mkdir /usr/local/mysql \
    && tar -zxf mariadb.tar.gz -C /usr/local/mysql --strip-components=1 \
    && rm -rf mariadb.tar.gz \
    && useradd -d /usr/local/mysql -M -s /sbin/nologin mysql \
    && chown -R www-data:www-data /usr/local/nginx \

EXPOSE 3306