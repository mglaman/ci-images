FROM circleci/php:7.2-apache-node-browsers
RUN sudo apt-get update && sudo apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libxml2-dev
RUN sudo docker-php-ext-install pdo_mysql mysqli mbstring opcache soap bcmath
RUN sudo docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && sudo docker-php-ext-install gd

# Install APCu and APC backward compatibility
RUN sudo pecl install apcu \
    && sudo  pecl install apcu_bc-1.0.3 \
    && sudo docker-php-ext-enable apcu --ini-name 10-docker-php-ext-apcu.ini \
    && sudo docker-php-ext-enable apc --ini-name 20-docker-php-ext-apc.ini
RUN composer global -q require "hirak/prestissimo:^0.3"
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/sh"]
