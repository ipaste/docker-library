FROM centos:6
MAINTAINER ChasonTang <chasontang@gmail.com>

# RUN cd /etc/yum.repos.d \
#     && mkdir backup \
#     && mv CentOS-Base.repo backup/ \
#     && curl "http://mirrors.aliyun.com/repo/Centos-6.repo" -o CentOS-Base.repo \
#     && curl "http://mirrors.aliyun.com/repo/epel-6.repo" -o epel.repo
RUN yum -y update; yum clean all
RUN yum -y groupinstall "Development Tools"; yum clean all
RUN yum -y install pcre-devel jemalloc-devel openssl-devel; yum clean all
ENV TENGINE_VERSION 2.1.2
RUN curl "http://tengine.taobao.org/download/tengine-$TENGINE_VERSION.tar.gz" -o tengine.tar.gz \
    && mkdir /usr/src/nginx \
    && tar -zxf tengine.tar.gz -C /usr/src/nginx --strip-components=1 \
    && rm -f tengine.tar.gz \
    && useradd -d /usr/local/nginx -M -s /sbin/nologin www-data \
    && cd /usr/src/nginx \
    && ./configure --user=www-data --group=www-data --with-file-aio --with-ipv6 --with-mail --with-mail_ssl_module \
    && make -j "$(nproc)" \
    && make install \
    && cd / \
    && rm -rf /usr/src/nginx \
    && chown -R www-data:www-data /usr/local/nginx \
# RUN echo "daemon off;" >> /usr/local/nginx/conf/nginx.conf
    && rm -f /usr/local/nginx/conf/nginx.conf
ADD nginx.conf /usr/local/nginx/conf/nginx.conf
RUN yum -y groupremove "Development Tools"; yum -y autoremove; yum clean all

# ENV PATH /usr/local/nginx/sbin:$PATH
WORKDIR /usr/local/nginx/html

EXPOSE 80
CMD ["/usr/local/nginx/sbin/nginx -s start"]