FROM java:openjdk-8u77-jre-alpine
MAINTAINER ChasonTang <chasontang@gmail.com>

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
ENV TOMCAT_MAJOR 8
ENV TOMCAT_VERSION 8.0.33
ENV TOMCAT_TGZ_URL https://www.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz

RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

RUN apk add --no-cache curl \
    && 