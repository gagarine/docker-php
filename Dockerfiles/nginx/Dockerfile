FROM debian:8

MAINTAINER Perdrisat Simon "perdrisat@gmail.com"

# Install dotdeb

ADD https://www.dotdeb.org/dotdeb.gpg /tmp/dotdeb.gpg

RUN echo "Install DotDeb" \
	&& echo "deb http://packages.dotdeb.org jessie all" > /etc/apt/sources.list.d/dotdeb.list \
	&& echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.list \
	&& apt-key add /tmp/dotdeb.gpg \
	&& rm /tmp/dotdeb.gpg \
	&& apt-get update && apt-get -y upgrade \
	&& echo "Common" \
	&& apt-get -y install apt-utils curl vim \
	&& echo "Install nginx" \
	&& apt-get -y install nginx \
	&& echo "\ndaemon off;" >> /etc/nginx/nginx.conf \
	&& echo "Cleanup" \
	&& apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false

COPY config/etc/nginx/sites-enabled/default /etc/nginx/sites-enabled/

EXPOSE 80
EXPOSE 443

CMD ["nginx"]