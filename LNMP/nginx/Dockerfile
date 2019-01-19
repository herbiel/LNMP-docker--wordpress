FROM centos:7
ENV TIME_ZOME Asia/Shanghai
ADD nginx-1.14.1.tar.gz /tmp

RUN \
    yum -y install gcc gcc-c++ make openssl-devel pcre-devel && \
    cd /tmp/nginx-1.14.1 && \
    ./configure --prefix=/usr/local/nginx --pid-path=/var/run/nginx/nginx.pid --lock-path=/var/lock/nginx.lock --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-http_gzip_static_module &&\
    make && make install && \
    rm -rf /tmp/nginx* && yum clean all && \
    echo "${TIME_ZOME}" > /etc/timezone && \
    mkdir -p /var/www/html && \ 
    ln -sf /usr/share/zoneinfo/${TIME_ZOME} /etc/localtime
RUN mkdir /usr/local/nginx/logs 
WORKDIR /usr/local/nginx
COPY nginx.conf conf/
EXPOSE 80
CMD ["./sbin/nginx","-g","daemon off;"]
