FROM node:4.4.3
MAINTAINER ChasonTang <chasontang@gmail.com>

ENV GHOST_VERSION 0.7.9
ENV GHOST_SOURCE /usr/src/ghost
ENV NODE_ENV production

WORKDIR $GHOST_SOURCE

RUN buildDeps=' \
        unzip \
    ' \
    && set -x \
    && apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
    && groupadd ghost && useradd -g ghost -r -s /sbin/nologin ghost \
    && mkdir -p "$GHOST_SOURCE" \
    && cd "$GHOST_SOURCE" \
    && curl -LO "https://ghost.org/zip/ghost-$GHOST_VERSION.zip" \
    && unzip ghost-$GHOST_VERSION.zip \
    && npm install --production \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false $buildDeps \
    && rm ghost-$GHOST_VERSION.zip \
    && npm cache clean \
    && rm -rf /tmp/npm* \
    && chown -R ghost:ghost "$GHOST_SOURCE/content"

COPY config.js /usr/src/ghost/config.js

EXPOSE 2368
CMD ["npm", "start"]