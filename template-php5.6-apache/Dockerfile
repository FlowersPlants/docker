FROM php:5.6-apache
COPY ./ /var/www/html/

RUN  \
  sed -i  's#http[:]//deb[^/ ]\+#http://ftp.cn.debian.org#g' /etc/apt/sources.list  && \
  apt-get update && apt-get install -y \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libpng-dev \
  && docker-php-ext-install iconv mcrypt \
  && docker-php-ext-configure gd \
  --enable-gd-native-ttf \
  --with-freetype-dir=/usr/include/freetype2 \
  --with-png-dir=/usr/include \
  --with-jpeg-dir=/usr/include \
  && docker-php-ext-install gd \
  && docker-php-ext-install mbstring \
  && docker-php-ext-enable gd \
  && docker-php-ext-install pdo_mysql mysqli

RUN chmod -R 777 /var/www/html/

CMD ["apache2-foreground"]
