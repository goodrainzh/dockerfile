FROM debian:stretch-slim

ENV NGINX_VERSION 1.12.2

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
	gcc \
	libpcre3 \
	libpcre3-dev \
	openssl \
	libssl-dev \
	perl \
	libperl-dev \
	zlib1g-dev \
	wget \
	&& rm -rf /var/lib/apt/lists/* \
	&& wget http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz \
    && tar -xzvf nginx-$NGINX_VERSION.tar.gz -C /usr/src \
    && cd /usr/src/nginx-$NGINX_VERSION \
    && ./configure \
		--prefix=/opt/goodrain/nginx\
		--with-ipv6 \
		--with-http_ssl_module \
		--with-http_realip_module \
		--with-http_addition_module \
		--with-http_dav_module \
		--with-http_flv_module \
		--with-http_mp4_module \
		--with-http_gzip_static_module \
		--with-http_perl_module \
		--with-mail \
		--with-mail_ssl_module \
  	  && make && make install

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]