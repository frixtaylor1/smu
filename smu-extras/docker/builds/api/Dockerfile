FROM php:8.0-apache

RUN a2enmod rewrite

COPY ../../../smu-api/.htaccess /var/www/html/.htaccess

COPY ../../../smu-api /var/www/html/

RUN echo "<Directory /var/www/html>\n\
    AllowOverride All\n\
    </Directory>" > /etc/apache2/conf-available/allowoverride.conf

RUN a2enconf allowoverride

RUN service apache2 restart
