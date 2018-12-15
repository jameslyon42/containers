FROM debian:stretch

RUN apt-get update && apt-get install -y \
	nginx \
	supervisor

RUN mkdir /var/www/public

ADD vhost.conf /etc/nginx/sites-available/default
ADD default.conf /etc/nginx/conf.d/default.conf

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80
CMD ["/usr/bin/supervisord"]