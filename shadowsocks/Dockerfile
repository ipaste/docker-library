FROM alpine:3.3
MAINTAINER ChasonTang <chasontang@gmail.com>

ENV SHADOWSOCKS_VERSION 2.4.6

RUN apk add --no-cache --virtual .build-deps \
        gcc \
        libc-dev \
        make \
        openssl-dev \
        zlib-dev \
        linux-headers \
        curl \
    && mkdir -p /usr/src \
    && cd /usr/src \
    && curl -LO "https://github.com/shadowsocks/shadowsocks-libev/archive/v$SHADOWSOCKS_VERSION.tar.gz" \
    && tar zxf v$SHADOWSOCKS_VERSION.tar.gz \
    && cd shadowsocks-libev-$SHADOWSOCKS_VERSION \
    && ./configure \
    && make \
    && make install \
    && runDeps="$( \
        scanelf --needed --nobanner /usr/local/bin/ss-server \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | sort -u \
            | xargs -r apk info --installed \
            | sort -u \
    )" \
    && apk add --virtual .nginx-rundeps $runDeps \
    && apk del .build-deps \
    && cd .. \
    && rm -rf v$SHADOWSOCKS_VERSION \
    && rm v$SHADOWSOCKS_VERSION

EXPOSE 8388
ENTRYPOINT ["/usr/local/bin/ss-server"]