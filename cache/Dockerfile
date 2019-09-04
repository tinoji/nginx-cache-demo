FROM alpine:3.10.2

ENV NGINX_VERSION 1.17.3
ENV NGINX_PURGE_VERSION 2.3

RUN apk update \
    && apk add gcc g++ make pcre pcre-dev zlib zlib-dev \
    && addgroup -g 101 -S nginx \
    && adduser -S -D -H -u 101 -h /var/cache/nginx -s /sbin/nologin -G nginx -g nginx nginx \
    && mkdir $HOME/build \
    && cd $HOME/build \
    && wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
    && wget http://labs.frickle.com/files/ngx_cache_purge-${NGINX_PURGE_VERSION}.tar.gz \
    && tar xzf nginx-${NGINX_VERSION}.tar.gz \
    && tar xzf ngx_cache_purge-${NGINX_PURGE_VERSION}.tar.gz \
    && cd $HOME/build/nginx-${NGINX_VERSION} \
    && ./configure \
        --user=nginx \
        --group=nginx \
        --add-module=$HOME/build/ngx_cache_purge-${NGINX_PURGE_VERSION} \
    && make \
    && make install

COPY nginx.conf /usr/local/nginx/conf/nginx.conf

EXPOSE 80

CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]

