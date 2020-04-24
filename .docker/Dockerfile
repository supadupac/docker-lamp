FROM php:7.4-apache
COPY ./app /var/www/html/
COPY .docker/vhost.conf /etc/apache2/sites-available/000-default.conf
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd
#install pecl and xdebug
RUN pecl install redis-5.1.1 \
    && pecl install xdebug-2.8.1 \
    && docker-php-ext-enable redis xdebug
#install pdo
RUN docker-php-ext-install pdo_mysql
#install mysql
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN chown -R www-data:www-data /var/www/html/ && a2enmod rewrite
RUN service apache2 restart

# docker build --file .docker/Dockerfile -t docker-tutorial .
# docker run -rm -p 8080:80 docker-tutorial
