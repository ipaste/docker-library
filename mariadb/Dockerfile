FROM alpine:3.3
MAINTAINER ChasonTang <chasontang@gmail.com>

ENV MARIADB_VERSION 10.1.13

ADD repositories /etc/apk/repositories

RUN apk add --no-cache --virtual .build-deps \
        curl \
    && addgroup -S mysql \
    && adduser -D -S -s /sbin/nologin -G mysql mysql \
    && curl -O "http://mirrors.aliyun.com/mariadb/mariadb-$MARIADB_VERSION/bintar-linux-x86_64/mariadb-$MARIADB_VERSION-linux-x86_64.tar.gz" \
    && tar -zxf mariadb-$MARIADB_VERSION-linux-x86_64.tar.gz -C /usr/local \
    && rm mariadb-$MARIADB_VERSION-linux-x86_64.tar.gz \
    && && apk del .build-deps

CMD []