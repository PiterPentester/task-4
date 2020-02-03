# My base ubuntu image

FROM ubuntu:18.04

ENV TZ=Europe/Kiev
ENV PHP_V 7.3
ENV SOFT nginx \
  supervisor \
  php${PHP_V}-fpm 
 

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
  && apt update -y \
  && apt install software-properties-common -y \
  && add-apt-repository ppa:ondrej/php -y \
  && apt-get update -y \
  && apt-get install ${SOFT} -y \
  && sed -i 's+/run/php/php7.3-fpm.sock+127.0.0.1:9000+g' /etc/php/7.3/fpm/pool.d/www.conf \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

COPY default /etc/nginx/sites-available/
COPY test.php /var/www/html/
COPY supervisord.conf /

EXPOSE 80
ENTRYPOINT ["/usr/bin/supervisord", "-c", "/supervisord.conf"]
