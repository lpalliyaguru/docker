FROM php:5.6-apache
# 1. Normal Update
RUN apt-get update -y && apt-get install -y libpng-dev curl libcurl4-openssl-dev libxml2-dev php-soap

# 2. Install Pdo, pdo_mysql, gd, curl, soap
RUN docker-php-ext-install pdo pdo_mysql gd curl soap

# 3. Install Redis PHP extension
# install phpredis extension
ENV PHPREDIS_VERSION 3.1.2

RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

# 4. Copy certificates
COPY my-dev.insead.edu.crt /etc/ssl/certs/
COPY my-dev.insead.edu.key /etc/ssl/private/
COPY my-dev.insead.edu.conf /etc/apache2/sites-available/

# 5. Apache reloading
RUN a2enmod rewrite
RUN service apache2 restart
RUN a2ensite my-dev.insead.edu.conf
RUN service apache2 restart
