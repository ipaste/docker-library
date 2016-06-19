FROM alpine:3.4

MAINTAINER ChasonTang <chasontang@gmail.com>

ENV TENGINE_VERSION 2.1.2_f
ENV CONFIG "\
        --prefix=/usr/local/nginx \
        --sbin-path=/usr/local/sbin/nginx \
        --conf-path=/etc/nginx/nginx.conf \
        --error-log-path=/usr/local/var/log/nginx/error.log \
        --pid-path=/usr/local/var/run/nginx.pid \
        --lock-path=/usr/local/var/run/nginx.lock \
        --user=nginx \
        --group=nginx \
        --with-file-aio \
        --with-ipv6 \
        --with-http_v2_module \
        --with-http_realip_module \
        --with-http_addition_module \
        --with-http_xslt_module=shared \
        --with-http_image_filter_module=shared \
        --with-http_geoip_module=shared \
        --with-http_sub_module=shared \
        --with-http_dav_module \
        --with-http_flv_module \
        --with-http_slice_module=shared \
        --with-http_mp4_module \
        --with-http_gunzip_module \
        --with-http_gzip_static_module \
        --with-http_auth_request_module \
        --with-http_concat_module \
        --with-http_random_index_module \
        --with-http_secure_link_module \
        --with-http_degradation_module \
        --with-http_sysguard_module=shared \
        --with-http_dyups_module \
        --http-log-path=/usr/local/var/log/nginx/access.log \
        --with-mail \
        --with-mail_ssl_module \
        --with-jemalloc \
        "

ADD ngx_user.patch /

RUN \
    addgroup -S nginx \
    && adduser -D -S -h /var/cache/nginx -s /sbin/nologin -G nginx nginx \
    && apk add --no-cache --virtual .build-deps \
        gcc \
        libc-dev \
        make \
        openssl-dev \
        pcre-dev \
        zlib-dev \
        linux-headers \
        curl \
        jemalloc-dev \
        libxslt-dev \
        gd-dev \
        geoip-dev \
    && curl -L "https://github.com/alibaba/tengine/archive/tengine-$TENGINE_VERSION.tar.gz" -o tengine.tar.gz \
    && mkdir -p /usr/src \
    && tar -zxC /usr/src -f tengine.tar.gz \
    && rm tengine.tar.gz \
    && cd /usr/src/tengine-tengine-$TENGINE_VERSION/src/os/unix/ \
    && mv /ngx_user.patch ./ngx_user.patch \
    && patch ngx_user.c ngx_user.patch \
    && rm ngx_user.patch \
    && cd ../../../ \
#    && cd /usr/src/tengine-$TENGINE_VERSION \
    && ./configure $CONFIG --with-debug \
    && make \
    && mv objs/nginx objs/nginx-debug \
    && mv objs/ngx_http_geoip_module.so objs/ngx_http_geoip_module-debug.so \
    && mv objs/ngx_http_image_filter_module.so objs/ngx_http_image_filter_module-debug.so \
    && mv objs/ngx_http_slice_module.so objs/ngx_http_slice_module-debug.so \
    && mv objs/ngx_http_sub_filter_module.so objs/ngx_http_sub_filter_module-debug.so \
    && mv objs/ngx_http_sysguard_module.so objs/ngx_http_sysguard_module-debug.so \
    && mv objs/ngx_http_xslt_filter_module.so objs/ngx_http_xslt_filter_module-debug.so \
    && ./configure $CONFIG \
    && make \
    && make install \
    && install -m755 objs/nginx-debug /usr/sbin/nginx-debug \
    && install -m755 objs/modules /usr/local/nginx/modules \
    && strip /usr/sbin/nginx* \
    && strip /usr/local/nginx/modules/*.so \
    && runDeps="$( \
        scanelf --needed --nobanner /usr/sbin/nginx /usr/local/nginx/modules/*.so \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | sort -u \
            | xargs -r apk info --installed \
            | sort -u \
    )" \
    && apk add --virtual .nginx-rundeps $runDeps \
    && apk del .build-deps \
    && rm -rf /usr/src/tengine-tengine-$TENGINE_VERSION \
    # forward request and error logs to docker log collector
    && ln -sf /dev/stdout /usr/local/var/log/nginx/access.log \
    && ln -sf /dev/stderr /usr/local/var/log/nginx/error.log

COPY nginx.conf /etc/nginx/nginx.conf
COPY nginx.vh.default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
