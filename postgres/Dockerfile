FROM alpine:3.4

MAINTAINER ChasonTang <chasontang@gmail.com>

ENV GOSU_VERSION 1.7
ENV LANG en_US.utf8
ENV PG_VERSION 9.5.3-r1
ENV PGDATA /var/lib/postgresql/data

RUN apk add --no-cache openssl \
    && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64" \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true \
    && apk del openssl \
    && mkdir /docker-entrypoint-initdb.d \
    && apk add --no-cache postgresql=$PG_VERSION postgresql-contrib=$PG_VERSION \
    && sed -ri "s!^#?(listen_addresses)\s*=\s*\S+.*!\1 = '*'!" /usr/share/postgresql/postgresql.conf.sample

VOLUME /var/lib/postgresql/data

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432

CMD ["postgres"]