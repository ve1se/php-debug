FROM php:7.3-apache

RUN apt-get update \
&&  apt-get install vim openssh-server mariadb-client mariadb-server -y \
&& echo 'root:root' | chpasswd \
&& curl -sS https://getcomposer.org/installer | php \
&& mv composer.phar /usr/local/bin/composer
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN pecl install xdebug-2.9.8
RUN docker-php-ext-enable xdebug
RUN echo "xdebug.remote_enable=1\nxdebug.remote_host=\"192.168.226.1\"\nxdebug.remote_port=9001\nxdebug.remote_handler=\"dbgp\"\nxdebug.idekey=zxhy\nxdebug.remote_autostart=1" >> /usr/local/etc/php/php.ini \
&& echo "PermitRootLogin  yes" >>  /etc/ssh/sshd_config \
&& echo "ServerName http://192.168.226.1:8000/">> /etc/apache2/apache2.conf
COPY ./start.sh /start.sh
EXPOSE 22
EXPOSE 8000
ENTRYPOINT ["/start.sh"]
