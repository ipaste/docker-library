FROM alpine:3.3
MAINTAINER ChasonTang <chasontang@gmail.com>

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 4.4.3

ADD repositories /etc/apk/repositories

RUN apk add --no-cache --virtual .build-deps \
        curl \
    && curl -LO "https://npm.taobao.org/mirrors/node/latest-v4.x/node-v$NODE_VERSION-linux-x64.tar.xz" \
    && tar -xJf node-v$NODE_VERSION-linux-x64.tar.xz -C /usr/local \
    && rm node-v$NODE_VERSION-linux-x64.tar.xz \
    && apk del .build-deps

CMD [ "node" ]