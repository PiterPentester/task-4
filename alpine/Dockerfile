# My alpine base image

FROM alpine:3.10

ENV PHP_V 7
ENV SOFT nginx \
 supervisor \
 curl \
 wget
ENV PHP_MOD php${PHP_V} \
 php${PHP_V}-fpm \
 php${PHP_V}-mysqli \
 php${PHP_V}-json \
 php${PHP_V}-openssl \
 php${PHP_V}-curl \
 php${PHP_V}-zlib \
 php${PHP_V}-xml \
 php${PHP_V}-phar \
 php${PHP_V}-intl \
 php${PHP_V}-dom \
 php${PHP_V}-xmlreader \
 php${PHP_V}-ctype \
 php${PHP_V}-session \
 php${PHP_V}-mbstring \
 php${PHP_V}-gd

RUN apk update \
  && apk --no-cache add ${SOFT} ${PHP_MOD} \
  && mkdir -p /run/nginx/ \
  && chown -R nobody:nobody /run \
  && chown -R nobody:nobody /var/lib/nginx \
  && chown -R nobody:nobody /var/tmp/nginx \
  && chown -R nobody:nobody /var/log/nginx \
  && chown -R nobody:nobody /var/log/php7

COPY --chown=nobody test.php /var/www/localhost/htdocs/
COPY --chown=nobody nginx.conf /etc/nginx/conf.d/default.conf
COPY --chown=nobody supervisord.conf /

USER nobody

EXPOSE 8080

ENTRYPOINT ["/usr/bin/supervisord", "-c", "/supervisord.conf"]
