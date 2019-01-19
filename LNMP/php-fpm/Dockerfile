FROM centos:7
MAINTAINER blog.51cto.com/ganbing
ENV TIME_ZOME Asia/Shanghai
RUN yum install -y gcc gcc-c++ make gd-devel libxml2-devel libcurl-devel libjpeg-devel libpng-devel openssl-devel
ADD php-5.6.38.tar.gz /tmp/
RUN   cd /tmp/php-5.6.38 && \
     ./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-mysql --with-mysqli --with-openssl --with-zlib --with-curl --with-gd  --with-jpeg-dir --with-png-dir --with-iconv --enable-fpm --enable-zip --enable-mbstring  && \    
     make -j 4 && \  
     make install && \
     cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf && \
     sed -i 's/127.0.0.1/0.0.0.0/g' /usr/local/php/etc/php-fpm.conf && \
     sed -i "21a daemonize=no" /usr/local/php/etc/php-fpm.conf && \
     echo "${TIME_ZOME}" > /etc/timezone && \
     ln -sf /usr/share/zoneinfo/${TIME_ZOME} /etc/localtime
RUN rm -rf /tmp/php* && yum clean all
WORKDIR /usr/local/php/
COPY php.ini-production etc/php.ini
EXPOSE 9000
CMD ["./sbin/php-fpm","-c","/usr/local/php/etc/php-fpm.conf"]
