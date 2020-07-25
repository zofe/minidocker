FROM nginx:1.13-alpine



ADD nginx.conf /etc/nginx/conf.d/default.conf

RUN apk --no-cache add curl
RUN echo http://dl-2.alpinelinux.org/alpine/edge/community/ >> /etc/apk/repositories

RUN apk --no-cache add shadow && usermod -u 1000 nginx && groupmod -g 1000 nginx

RUN chown -R nginx.nginx /var/log/nginx

WORKDIR /application



