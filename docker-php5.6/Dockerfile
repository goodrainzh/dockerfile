FROM goodrainapps/debian:jessie-20171210

ENV PHP_VERSION=5.6.32
ENV PHP_DIR=/opt/goodrain/php-fpm
ENV PATH=$PATH:${PHP_DIR}/bin
ENV DOWNLOAD_URL=https://pkg.goodrain.com/grstack/debian

RUN apt-get update \
    && apt-get install -y libedit2 libxml2 \
    && rm -r /var/lib/apt/lists/*

RUN curl -k ${DOWNLOAD_URL}/php-${PHP_VERSION}-fpm.tar.gz | tar xz -C /

RUN set -x \
    && groupadd  -g 200 rain \
    && useradd -u 200 -g 200 rain 

EXPOSE 80

VOLUME [ "/data" ]

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT [ "/docker-entrypoint.sh" ]