FROM debian:stretch

RUN apt-get update && apt-get install -y \
	apt-transport-https \
	lsb-release \
	ca-certificates \
	wget

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
	sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

RUN apt-get update && apt-get install -y \
	nginx \
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

RUN mkdir -p /run/php && touch /run/php/php7.2-fpm.sock && touch /run/php/php7.2-fpm.pid

RUN mkdir /var/www/site

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD vhost.conf /etc/nginx/sites-available/default

EXPOSE 80
CMD ["/usr/bin/supervisord"]