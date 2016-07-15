FROM debian:8

MAINTAINER Perdrisat Simon "perdrisat@gmail.com"


# Install phpfpm via dotdeb

ADD https://www.dotdeb.org/dotdeb.gpg /tmp/dotdeb.gpg

RUN echo "Install DotDeb" \
	&& echo "deb http://packages.dotdeb.org jessie all" > /etc/apt/sources.list.d/dotdeb.list \
	&& echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.list \
	&& apt-key add /tmp/dotdeb.gpg \
	&& rm /tmp/dotdeb.gpg \
	&& apt-get update && apt-get -y upgrade \
	&& echo "Common" \
	&& DEBIAN_FRONTEND="noninteractive" apt-get -y install curl vim \
	&& echo "Install PHP" \
	&& DEBIAN_FRONTEND="noninteractive" apt-get -y install php7.0 php7.0-cli php7.0-fpm php7.0-readline php7.0-redis php7.0-curl php7.0-gd php-xml php7.0-intl php7.0-mcrypt php7.0-mysql php7.0-memcached

# sSMTP
# note php is configured to use ssmtp, which is configured to send to mail:1025,
# which is standard configuration for a mailhog/mailhog image with hostname mail.
RUN DEBIAN_FRONTEND="noninteractive" apt-get install --yes ssmtp

RUN cp /etc/ssmtp/ssmtp.conf /etc/ssmtp/ssmtp.conf.dist
COPY ./config/etc/ssmtp/ssmtp.conf /etc/ssmtp/ssmtp.conf

RUN cp /etc/php/7.0/fpm/php.ini /etc/php/7.0/fpm/php.ini.dist
COPY ./config/etc/php/7.0/fpm/php.ini /etc/php/7.0/fpm/

RUN cp /etc/php/7.0/fpm/php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf.dist
COPY config/etc/php/7.0/fpm/php-fpm.conf /etc/php/7.0/fpm/

# missing folder for the socket. 
# Avoid ERROR: unable to bind listening socket for address '/run/php/php7.0-fpm.sock
RUN mkdir -p run/php

EXPOSE 9000
CMD ["php-fpm7.0", "--nodaemonize"]
