FROM chasontang/swift:3.0.1
MAINTAINER ChasonTang <chasontang@gmail.com>

COPY . /usr/local/src/Ghost
WORKDIR /usr/local/src/Ghost
RUN apt-get install -y libssl-dev uuid-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && swift build -c release

CMD .build/release/Ghost --port 8080