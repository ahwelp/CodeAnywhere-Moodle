FROM php:7.4-apache

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
# Enable .htaccess files & mod_rewrite
RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride all/' /etc/apache2/apache2.conf
RUN a2enmod rewrite

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends git ssh-client postgresql; \
	rm -rf /var/lib/apt/lists/*

RUN set -eux; \
    apt-get install \ 
    php7.4-pgsql \
    php7.4-xml \ 
    php7.4-mbstring \ 
    php7.4-curl \ 
    php7.4-zip \
    php7.4-gd \
    php7.4-gd \
    php7.4-intl \
    php7.4-xmlrpc \
    php7.4-soap \
    php7.4-ldap \
    rm -rf /var/lib/apt/lists/*

#add vscode user
RUN useradd -ms /bin/bash vscode \
		&& usermod -aG www-data vscode

WORKDIR /var/www/html
USER www-data

RUN git clone https://github.com/moodle/moodle.git

USER root
RUN chown -R www-data:www-data /var/www/html/
RUN chmod g+w -R /var/www/html/