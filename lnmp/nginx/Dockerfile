FROM centos:7
LABEL maintainer www.ctnrs.com
RUN yum install -y gcc gcc-c++ make \
    openssl-devel pcre-devel gd-devel \
	iproute net-tools telnet wget curl && \
	yum clean all && \
	rm -rf /var/cache/yum/*
RUN wget http://nginx.org/download/nginx-1.15.5.tar.gz && \
    tar xzf nginx-1.15.5.tar.gz
RUN cd nginx-1.15.5 && \
    ./configure --prefix=/usr/local/nginx \
    --with-http_ssl_module \
    --with-http_stub_status_module && \
    make -j 4 && make install && \
    mkdir /usr/local/nginx/conf/vhost && \
    cd / && rm -rf nginx* && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
ENV PATH $PATH:/usr/local/nginx/sbin
COPY nginx.conf /usr/local/nginx/conf/nginx.conf
WORKDIR /usr/local/nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
