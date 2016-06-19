FROM alpine:3.4
MAINTAINER ChasonTang <chasontang@gmail.com>

ENV GOSU_VERSION 1.7
ENV LANG en_US.utf8
ENV PG_MAJOR 9.5
ENV PG_VERSION 9.5.3-r1

RUN apk add --no-cache curl \
    && curl -o /usr/local/bin/gosu -fsSL "https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64" \
    && chmod +x /usr/local/bin/gosu \
    && apk del curl \
    && mkdir /docker-entrypoint-initdb.d \
    && apk add --no-cache postgresql=$PG_VERSION \

ENV PGDATA /var/lib/postgresql/data
VOLUME /var/lib/postgresql/data

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]