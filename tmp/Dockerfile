FROM nginx

RUN apt-get update -y \
    && apt-get install -y iputils-ping net-tools dnsutils curl wget

COPY nginx.conf /etc/nginx/nginx.conf

