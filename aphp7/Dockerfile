#Download base image ubuntu 16.04
FROM ubuntu:18.04

ENV TZ=Europe/Stockholm
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
ARG DEBIAN_FRONTEND=noninteractive

# Update Ubuntu Software repository
RUN apt-get update

# Install nginx, php-fpm and supervisord from ubuntu repository
RUN apt-get install -y apache2 php7.2 imagemagick xvfb libfontconfig wkhtmltopdf

#Define the ENV variable
ENV apache_vhost /etc/apache2/sites-available/000-default.conf
ENV php_conf /etc/php/7.2/apache2/php.ini
#ENV nginx_conf /etc/nginx/nginx.conf
#ENV supervisor_conf /etc/supervisor/supervisord.conf
 
# Enable php-fpm on nginx virtualhost configuration
COPY 000-default.conf ${apache_vhost}

RUN chown -R www-data:www-data /var/www/html

# Volume configuration
VOLUME ["/etc/apache2/sites-enabled", "/etc/apache2/conf.d", "/var/log/apache2", "/var/www/html"]

# Configure Services and Port
 
EXPOSE 80
cmd apachectl -D FOREGROUND
