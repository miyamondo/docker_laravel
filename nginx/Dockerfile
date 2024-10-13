FROM nginx:1.25.3-alpine3.18

RUN apk --update add tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

# install packages
RUN apk update && \
    apk upgrade && \
    apk add --update --no-cache \
    bash \
    nginx \
    sudo \
    tzdata \
    vim

COPY ./conf/nginx.conf /etc/nginx/nginx.conf
COPY ./conf/dev-laravel.menta.work.conf /etc/nginx/conf.d/dev-laravel.menta.work.conf

EXPOSE 80
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]