FROM nginx

RUN apt-get update -y \
    && apt-get install -y iputils-ping net-tools dnsutils curl \
    && mkdir /usr/share/nginx/html/static

COPY static /usr/share/nginx/html/static
