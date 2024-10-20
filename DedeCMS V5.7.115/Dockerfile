FROM php:7.4-apache

RUN docker-php-ext-install mysqli pdo pdo_mysql

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    unzip \
    curl && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd

WORKDIR /var/www/html

RUN curl -o DedeCMS.zip https://updatenew.dedecms.com/base-v57/package/DedeCMS-V5.7.115-UTF8.zip && \
    unzip DedeCMS.zip -d /var/www/html && \
    rm DedeCMS.zip

RUN chown -R www-data:www-data /var/www/html

EXPOSE 80

RUN service apache2 restart

CMD ["apache2-foreground"]
