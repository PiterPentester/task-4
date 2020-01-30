# My base ubuntu image

FROM ubuntu:18.04

ENV TZ=Europe/Kiev
ENV PHP_V 7.3
ENV SOFT nginx \
  supervisor \
  php${PHP_V}-fpm \
  php${PHP_V}-common \
  php${PHP_V}-mysql \
  php${PHP_V}-xml \
  php${PHP_V}-xmlrpc \
  php${PHP_V}-curl \
  php${PHP_V}-gd \
  php${PHP_V}-imagick \
  php${PHP_V}-cli \
  php${PHP_V}-dev \
  php${PHP_V}-imap \
  php${PHP_V}-mbstring \
  php${PHP_V}-opcache \
  php${PHP_V}-soap \
  php${PHP_V}-zip \
  php${PHP_V}-intl \
  curl \
  wget

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
  && apt update && apt upgrade -y \
  && apt install software-properties-common -y \
  && add-apt-repository ppa:ondrej/php -y \
  && apt-get update && apt-get upgrade -y \
  && apt-get install ${SOFT} -y \
  && sed -i 's+/run/php/php7.3-fpm.sock+127.0.0.1:9000+g' /etc/php/7.3/fpm/pool.d/www.conf \
  && apt-get clean

COPY default /etc/nginx/sites-available/
COPY test.php /var/www/html/
COPY supervisord.conf /

EXPOSE 80
ENTRYPOINT ["/usr/bin/supervisord", "-c", "/supervisord.conf"]
