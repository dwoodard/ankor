FROM ubuntu:14.04
MAINTAINER Dustin Woodard <dustin.woodard@gmail.com>

RUN apt-get update && apt-get install -y \
 curl \
 apache2 \
 && apt-get clean

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

# ------------------ Make CERT. ------------------
RUN openssl req -new -newkey rsa:4096 -days 3652 -nodes -x509 -subj "/C=US/ST=UT/L=Ogden/O=IT/CN=vagrant.dev" -keyout /var/www/server.pem  -out /var/www/server.cert

ADD "app.conf" /etc/apache2/sites-available/

ADD a2ensite /etc/apache2/sites-available/app.conf
ADD a2enmod ssl

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]

