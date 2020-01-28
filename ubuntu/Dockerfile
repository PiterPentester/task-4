# My base ubuntu image

FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade -y \
  && apt install nginx -y \
  && apt-get install software-properties-common -y \
  && add-apt-repository ppa:ondrej/php -y \
  && apt-get update \
  && apt-get install php7.4-fpm -y \
  && apt-get clean

EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
