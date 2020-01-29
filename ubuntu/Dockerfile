# My base ubuntu image

FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade -y \
  && apt install nginx supervisor -y \
  && apt-get install software-properties-common -y \
  && add-apt-repository ppa:ondrej/php -y \
  && apt-get update \
  && apt-get install php7.4-fpm -y \
  && sed -i 's+/run/php/php7.4-fpm.sock+127.0.0.1:9000+g' /etc/php/7.4/fpm/pool.d/www.conf \
  && apt-get clean

COPY default /etc/nginx/sites-available/
COPY test.php /var/www/html/
COPY supervisord.conf /

EXPOSE 80
ENTRYPOINT ["/usr/bin/supervisord", "-c", "/supervisord.conf"]
