FROM debian:stretch

RUN apt-get update && apt-get install -y \
	apt-transport-https \
	lsb-release \
	ca-certificates \
	wget \
	curl \
	gnupg2

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
	sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -

RUN apt-get update && apt-get install -y \
	php7.2-fpm \
	php7.2-pdo \
	php7.2-mysql \
	php7.2-mbstring \
	php7.2-xml \
	php-xdebug \
	zip \
	unzip \
	supervisor \
	npm \
	libpng-dev \
	make \
	gcc

RUN sed -i 's/\/run\/php\/php7.2-fpm.sock/0.0.0.0:9000/' /etc/php/7.2/fpm/pool.d/www.conf

RUN mkdir -p /var/www/

RUN php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');" && \
    php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('/tmp/composer-setup.php'); } echo PHP_EOL;" && \
    php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer

RUN npm i npm@6.1.0 -g

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD 90-blog.ini /etc/php/7.2/fpm/conf.d/90-blog.ini

WORKDIR /var/www

EXPOSE 9000
CMD ["/usr/bin/supervisord"]