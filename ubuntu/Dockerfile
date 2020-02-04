# My base ubuntu image

FROM ubuntu:18.04

ENV TZ=Europe/Kiev
ENV PHP_V 7.3
ENV SOFT nginx \
  supervisor \
  php${PHP_V}-fpm 
 

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
  && apt-get update -y && apt-get upgrade -y \
  && apt-get install --no-install-recommends software-properties-common -y \
  && add-apt-repository ppa:ondrej/php -y \
  && apt-get install --no-install-recommends ${SOFT} -y \
  && sed -i 's+/run/php/php7.3-fpm.sock+127.0.0.1:9000+g' /etc/php/7.3/fpm/pool.d/www.conf \
  && sed -i 's/;daemonize = yes/daemonize = no/g' /etc/php/7.3/fpm/php-fpm.conf \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && groupadd -g 1000 user \
  && useradd -s /bin/bash -d /home/user/ -u 1000 -g 1000 user \
  && mkdir /home/user/ \
  && mkdir /run/php \
  && chown -R user:user /home/user \
  && chown -R user:user /run \
  && chown -R user:user /var/lib/nginx \
  && chown -R user:user /var/log/ \
  && chown -R user:user /etc/php/7.3/fpm/php-fpm.conf

COPY --chown=user default /etc/nginx/sites-available/
COPY --chown=user test.php /var/www/html/
COPY --chown=user supervisord.conf /home/user

EXPOSE 8080

USER user
ENTRYPOINT ["/usr/bin/supervisord", "-c", "/home/user/supervisord.conf"]
