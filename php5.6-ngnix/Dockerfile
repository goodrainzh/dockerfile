FROM goodrainapps/debian:jessie-20171210

ENV PHP_VERSION=5.6.32
ENV NGINX_VERSION=1.12.2
ENV PHP_DIR=/opt/goodrain/php-fpm
ENV NGINX_DIR=/opt/goodrain/ngnix-$NGINX_VERSION
ENV PATH=$PATH:${PHP_DIR}/bin:${NGINX_DIR}/bin
ENV DOWNLOAD_URL=https://pkg.goodrain.com/grstack/debian

RUN apt-get update \
#php depence
    && apt-get install -y libedit2 libxml2 \
    && rm -r /var/lib/apt/lists/*

RUN set -x \
    && curl -k ${DOWNLOAD_URL}/php-${PHP_VERSION}-fpm.tar.gz | tar xz -C / \
    && curl -k ${DOWNLOAD_URL}/php-${NGINX_VERSION}-fpm.tar.gz | tar xz -C /

RUN set -x \
    && groupadd  -g 200 rain \
    && useradd -u 200 -g 200 rain \
    && mkdir -p /data \
    && echo "<?php\nphpinfo();\n?>" > /data/index.php

EXPOSE 80

VOLUME [ "/data" ]

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT [ "/docker-entrypoint.sh" ]