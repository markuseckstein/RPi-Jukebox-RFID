FROM alpine:latest


RUN apk --update add \
  lighttpd \
  php7 \
  php7-common \
  php7-cgi \
  php7-fpm \
  fcgi \
  && rm -rf /var/cache/apk/*

ADD lighttpd.conf /etc/lighttpd/lighttpd.conf
ADD htdocs /var/www/web

RUN mkdir -p /var/www/web/ && \ 
  echo "<?php phpinfo();" > /var/www/web/index.php && \
  adduser www-data -G www-data -H -s /bin/false -D && \
  #ln -s /usr/bin/php-cgi7 /usr/bin/php-cgi && \
  #ln -s /usr/bin/php7 /usr/bin/php && \
  mkdir -p /run/lighttpd/ && \
  chown www-data. /run/lighttpd/

EXPOSE 80

CMD php-fpm7 -D && lighttpd -D -f /etc/lighttpd/lighttpd.conf