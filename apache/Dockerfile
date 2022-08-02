FROM ubuntu:20.04

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    rm -rf /var/lib/apt/lists/* &&\
    add-apt-repository ppa:ondrej/php &&\
    apt install -y git unzip apache2\
    php7.4\
    curl php7.4-fpm \
    php7.4-curl\
    php7.4-mbstring\
    php7.4-ldap\
	php7.4-tidy\
	php7.4-xml\
	php7.4-zip\
	php7.4-gd\
	php7.4-mysql\
	libapache2-mod-php7.4\
	php7.4-cli\
	php7.4-sqlite3

COPY /bookstack /var/www/bookstack

COPY bookstack.conf /etc/apache2/sites-available/

RUN chown -R www-data:www-data /var/www/bookstack/ && chmod -R 755 /var/www/bookstack

RUN a2enmod rewrite &&\
	a2enmod php7.4 &&\
	a2ensite bookstack.conf &&\
	a2dissite 000-default.conf &&\
	service apache2 restart

EXPOSE 80

#CMD ["apachectl", "-D", "FOREGROUND"]

