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
    php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('/tmp/composer-setup.php'); } echo PHP_EOL;" && \
    php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer

RUN npm i npm@6.1.0 -g

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

WORKDIR /var/www

EXPOSE 9000
CMD ["/usr/bin/supervisord"]