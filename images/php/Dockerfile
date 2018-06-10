FROM debian:stretch

RUN apt-get update && apt-get install -y \
	apt-transport-https \
	lsb-release \
	ca-certificates \
	wget

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
	sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

RUN apt-get update && apt-get install -y \
	php7.2-fpm \
	php7.2-pdo \
	php7.2-mysql \
	php7.2-mbstring \
	php7.2-xml \
	composer \
	curl \
	zip \
	unzip \
	supervisor

RUN sed -i 's/\/run\/php\/php7.2-fpm.sock/0.0.0.0:9000/' /etc/php/7.2/fpm/pool.d/www.conf

RUN mkdir -p /var/www/site/

WORKDIR /var/www/site/

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 9000
CMD ["/usr/bin/supervisord"]