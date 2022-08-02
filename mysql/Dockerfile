FROM ubuntu:20.04

VOLUME /etc/lib/mysql

#Ручная настройка времени для вопроса при установки пакетоввсщлук
#ENV TZ=Europe/Moscow
#RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update &&\
    apt-get install\
    mysql-server\
    mysql-client\
    mysql-server -y

COPY mdump.sql /var/lib/mysql

RUN usermod -d /var/lib/mysql/ mysql &&\
	sed -i "s/127.0.0.1/0.0.0.0/g" /etc/mysql/mysql.conf.d/mysqld.cnf

RUN etc/init.d/mysql start &&\
	mysql -u root --execute="CREATE DATABASE bookstack;" && \
	mysql -u root --execute="CREATE USER 'bookstack'@'%' IDENTIFIED WITH mysql_native_password BY 'password';"  &&\
	mysql -u root -ppassword bookstack < /var/lib/mysql/mdump.sql 
	
EXPOSE 3306

#CMD ["mysqld_safe"]











