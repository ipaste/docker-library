FROM swiftdocker/swift:3.0.1
MAINTAINER ChasonTang <chasontang@gmail.com>

RUN apt-get update \
    && apt-get install -y uuid-dev \ 
    && git clone https://github.com/PerfectlySoft/PerfectTemplate /usr/src/PerfectTemplate \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
WORKDIR /usr/src/PerfectTemplate
RUN swift build -c release
CMD .build/release/PerfectTemplate --port 80