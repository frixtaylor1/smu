FROM php:apache

RUN a2enmod rewrite

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable mysqli


COPY ./smu-api/.htaccess /var/www/html/.htaccess

COPY ./smu-api /var/www/html/

RUN chmod 600 /var/www/html/.env 

RUN echo "<Directory /var/www/html>\n\
    AllowOverride All\n\
    </Directory>" > /etc/apache2/conf-available/allowoverride.conf

RUN a2enconf allowoverride

RUN service apache2 restart
