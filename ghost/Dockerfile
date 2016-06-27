FROM chasontang/node:4.4.4
MAINTAINER ChasonTang <chasontang@gmail.com>

ENV GHOST_VERSION 0.8.0
ENV GHOST_SOURCE /usr/src/ghost
ENV GHOST_CONTENT /var/lib/ghost
ENV NODE_ENV production

WORKDIR $GHOST_SOURCE

RUN addgroup -S ghost \
    && adduser -h $GHOST_SOURCE -S -G ghost ghost \
    && apk add --no-cache curl \
    && cd $GHOST_SOURCE \
    && curl -o ghost.zip "https://ghost.org/archives/ghost-$GHOST_VERSION.zip" \
    && apk del curl \
    && unzip ghost.zip \
    && npm install --production \
    && rm ghost.zip \
    && npm cache clean \
    && rm -rf /tmp/npm* \
    && mkdir -p "$GHOST_CONTENT" \
    && chown -R ghost:ghost "$GHOST_CONTENT"

VOLUME $GHOST_CONTENT

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 2368
CMD ["npm", "start"]