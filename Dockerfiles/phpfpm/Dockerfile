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
	&& DEBIAN_FRONTEND="noninteractive" apt-get -y install php5-fpm php5-cli php5-gd php5-intl php5-curl php5-mysql php5-redis php5-mcrypt php5-common php5-memcached

# sSMTP
# note php is configured to use ssmtp, which is configured to send to mail:1025,
# which is standard configuration for a mailhog/mailhog image with hostname mail.
RUN DEBIAN_FRONTEND="noninteractive" apt-get install --yes ssmtp

RUN cp /etc/ssmtp/ssmtp.conf /etc/ssmtp/ssmtp.conf.dist
COPY ./config/etc/ssmtp/ssmtp.conf /etc/ssmtp/ssmtp.conf

RUN cp /etc/php5/fpm/php.ini /etc/php5/fpm/php.ini.dist
COPY ./config/etc/php5/fpm/php.ini /etc/php5/fpm/

RUN cp /etc/php5/fpm/php-fpm.conf /etc/php5/fpm/php-fpm.conf.dist
COPY config/etc/php5/fpm/php-fpm.conf /etc/php5/fpm/

# missing folder for the socket.
# Avoid ERROR: unable to bind listening socket for address '/run/php/php7.0-fpm.sock
RUN mkdir -p run/php

EXPOSE 9000
CMD ["php5-fpm", "--nodaemonize"]
