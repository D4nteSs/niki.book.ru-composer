FROM ubuntu:20.04

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    rm -rf /var/lib/apt/lists/* &&\
    add-apt-repository ppa:ondrej/php &&\
    apt install -y git \
	wget \ 
	unzip \
	apache2 \
	curl \
	php8.2 \
	php8.2-curl \
	php8.2-mbstring \
	php8.2-ldap \
	php8.2-xml \
	php8.2-zip \
	php8.2-gd \
	php8.2-mysql \
	mysql-server-8.0 \
	libapache2-mod-php8.2

RUN sed -i -e '1 s/^/Listen 8888\n/;' /etc/apache2/ports.conf

WORKDIR /var/www

RUN wget https://github.com/BookStackApp/BookStack/archive/refs/tags/v22.11.zip  &&\
    unzip v22.11.zip &&\
    mv BookStack-22.11/ bookstack &&\
    cd bookstack &&\
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" &&\
    php composer-setup.php --quiet &&\
    mv composer.phar /usr/local/bin/composer &&\
    export COMPOSER_ALLOW_SUPERUSER=1 &&\
    php /usr/local/bin/composer install --no-dev --no-plugins &&\ 
    cp .env.example .env &&\
    sed -i.bak "s@APP_URL=.*\$@APP_URL=${APP_URL}@" .env &&\
    sed -i 's/localhost/mysql/' .env &&\
    sed -i 's/database_database/${MYSQL_DATABASE}/' .env &&\
    sed -i 's/database_username/${MYSQL_USER}/' .env &&\
    sed -i 's/database_user_password/${MYSQL_PASSWORD}/' .env &&\
    echo 'APP_DEBUG=true' >> .env &&\
    php artisan key:generate --no-interaction --force 
    #php artisan migrate --no-interaction --force

COPY bookstack.conf /etc/apache2/sites-available/bookstack.conf

RUN sed -i 's/ServerName/ServerName ${APP_URL}/' /etc/apache2/sites-available/bookstack.conf 

WORKDIR /var/www/bookstack

RUN chown -R www-data:www-data /var/www/bookstack/ && chmod -R 755 /var/www/bookstack

RUN a2enmod rewrite &&\
	a2enmod php8.2 &&\
	a2ensite bookstack.conf &&\
	a2dissite 000-default.conf &&\
	service apache2 restart

EXPOSE 80


