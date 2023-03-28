FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update &&\
    apt-get install\
    mysql-server\
    mysql-client\
    mysql-server -y

RUN usermod -d /var/lib/mysql/ mysql &&\
	sed -i "s/127.0.0.1/0.0.0.0/g" /etc/mysql/mysql.conf.d/mysqld.cnf


ENV MYSQL_NAME=bookstack\
    MYSQL_USER=bookstack\
    MYSQL_PASSWORD=qwerty12345
 

RUN etc/init.d/mysql start &&\
	mysql -u root -e "CREATE DATABASE ${MYSQL_USER}" &&\  
	mysql -u root -e "CREATE USER '${MYSQL_USER}'@'%' IDENTIFIED WITH mysql_native_password BY '${MYSQL_PASSWORD}';" &&\
	mysql -u root -e "GRANT ALL PRIVILEGES ON ${MYSQL_DATABASE}.* TO '${MYSQL_USER}'@'%';" 
        #FLUSH PRIVILEGES;"

EXPOSE 3306

CMD ["mysqld_safe"]











