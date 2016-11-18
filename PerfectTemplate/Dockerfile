FROM chasontang/swift:3.0.1
MAINTAINER ChasonTang <chasontang@gmail.com>

RUN git clone https://github.com/PerfectlySoft/PerfectTemplate /usr/src/PerfectTemplate
WORKDIR /usr/src/PerfectTemplate
RUN swift build -c release
CMD .build/release/PerfectTemplate --port 80