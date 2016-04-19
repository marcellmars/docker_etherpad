FROM librarian/motw

MAINTAINER Marcell Mars "https://github.com/marcellmars"

#---- this is convenient setup with cache for local development ---------------
# RUN echo 'Acquire::http::Proxy "http://172.17.42.1:3142";' >> /etc/apt/apt.conf.d/01proxy

RUN apt-get update &&\
    apt-get install -y software-properties-common

RUN add-apt-repository ppa:nginx/stable -y

RUN apt-get update
RUN apt-get install -y nginx

ADD nginx.conf /etc/supervisor/conf.d/
ADD gzip.conf /etc/nginx/conf.d/
ADD ssl.conf /etc/nginx/conf.d/

RUN mkdir -p /etc/nginx/docker_volumes
ADD etc_nginx.conf /etc/nginx/nginx.conf

ADD pad.labinary.org.crt /etc/ssl/certs/pad.labinary.org.crt
ADD pad.labinary.org.key /etc/ssl/private/pad.labinary.org.key
RUN chmod 600 /etc/ssl/certs/pad.labinary.org.crt
RUN chmod 600 /etc/ssl/private/pad.labinary.org.key

ADD dhparam.pem /etc/ssl/private/dhparam.pem

ADD dnsmasq.local /etc/dnsmasq.d/local

RUN mkdir -p /var/www/cache
RUN chmod -R ugo+rwx /var/www/cache

ADD default_domains /etc/nginx/sites-enabled/

ADD static_web/ /var/www/
