# My base centos7 image

FROM centos:centos7

ENV TZ=Europe/Kiev
ENV PHP_V 73
ENV PHP_MOD php-fpm \
  php-common \
  php-mysql \
  php-xml \
  php-xmlrpc \
  php-curl \
  php-gd \
  php-imagick \
  php-cli \
  php-dev \
  php-imap \
  php-mbstring \
  php-opcache \
  php-soap \
  php-zip \
  php-intl
 
ENV SOFT curl \
  supervisor \
  nginx \
  wget

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
  && yum install epel-release -y \
  && rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm \
  && yum update -y \
  && yum --enablerepo=remi-php${PHP_V} install -y ${PHP_MOD} \
  && yum install ${SOFT} -y \
  && mkdir -p /run/php-fpm/ \
  && yum clean all -y

COPY nginx.conf /etc/nginx/
COPY supervisord.conf /
COPY index.php /var/www/

EXPOSE 80
ENTRYPOINT ["/usr/bin/supervisord", "-c", "/supervisord.conf"]
