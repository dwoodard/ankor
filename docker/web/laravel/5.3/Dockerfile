FROM php:7.1-apache

MAINTAINER Dustin Woodard <dustin.woodard@gmail.com>

#  Installs Utils and Apache

RUN mkdir -p /var/www 
RUN usermod -u 1000 www-data 
RUN usermod -a -G users www-data 
RUN chown -R www-data:www-data /var/www/ 




# Setting document root
RUN mkdir /var/www/html/public/
RUN sed -i "s#.*DocumentRoot /var/www/html#\tDocumentRoot /var/www/html/public#" /etc/apache2/sites-enabled/000-default.conf
RUN sed -i "s#\#ServerName www.example.com#ServerName localhost#" /etc/apache2/sites-enabled/000-default.conf

# Composer is the future. But you knew that did you Nice job.
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" 
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === 'aa96f26c2b67226a324c27919f1eb05f21c248b987e6195cad9690d5c1ff713d53020a02ac8c217dbf90a7eacc9d141d') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" 
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer 
RUN php -r "unlink('composer-setup.php');"

# Correct Time
RUN echo "America/Denver" | tee /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN mkdir -p /etc/ssl/server/certs


#ADD app.conf /etc/apache2/sites-available/

#RUN a2ensite app.conf
RUN a2enmod ssl

VOLUME ["/var/www/html/"]

EXPOSE 80
EXPOSE 443

CMD /usr/sbin/apache2ctl -D FOREGROUND
