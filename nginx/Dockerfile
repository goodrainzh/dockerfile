FROM debian:stretch-slim

ENV TZ=Asia/Shanghai
ENV PCRE_VERSION=8.41
ENV ZLIB_VERSION=1.2.11
ENV OPENSSL_VERSION=1.1.0g
ENV NGINX_VERSION=1.12.2
ENV BUILD_DIR=/opt/goodrain/nginx-${NGINX_VERSION}
ENV DEBUG=1

RUN mkdir -p $BUILD_DIR \
    && apt-get update \
    && apt-get install -y --no-install-recommends  build-essential wget 

# pcre install
RUN cd $BUILD_DIR \
    && wget http://goodrain-pkg.oss-cn-shanghai.aliyuncs.com/dockerfile/ngnix/pcre-$PCRE_VERSION.tar.gz \
    && tar -zxvf pcre-$PCRE_VERSION.tar.gz \
    && rm -rf $BUILD_DIR/pcre-$PCRE_VERSION.tar.gz \
    && cd pcre-$PCRE_VERSION \
    && ./configure --prefix=$BUILD_DIR/libpcre \
    && make && make install

# zlib install
RUN cd $BUILD_DIR \
    && wget http://goodrain-pkg.oss-cn-shanghai.aliyuncs.com/dockerfile/ngnix/zlib-$ZLIB_VERSION.tar.gz \
    && tar -zxvf zlib-$ZLIB_VERSION.tar.gz \
    && rm -rf zlib-$ZLIB_VERSION.tar.gz \
    && cd zlib-$ZLIB_VERSION \
    && ./configure --prefix=$BUILD_DIR/libzip \
    && make && make install

# openssl install
RUN cd $BUILD_DIR \
    && wget http://goodrain-pkg.oss-cn-shanghai.aliyuncs.com/dockerfile/ngnix/openssl-${OPENSSL_VERSION}.tar.gz \
    && tar -zxvf openssl-${OPENSSL_VERSION}.tar.gz \
    && rm -rf 
# nginx install
RUN cd $BUILD_DIR \
    && wget http://goodrain-pkg.oss-cn-shanghai.aliyuncs.com/dockerfile/ngnix/nginx-${NGINX_VERSION}.tar.gz \
    && tar -zxvf nginx-$NGINX_VERSION.tar.gz \
    && rm -rf nginx-$NGINX_VERSION.tar.gz \
    && cd nginx-$NGINX_VERSION \
    && ./configure \
    --prefix=$BUILD_DIR \
    --with-http_ssl_module \
    --with-pcre=$BUILD_DIR/pcre-$PCRE_VERSION \
    --with-zlib=$BUILD_DIR/zlib-$ZLIB_VERSION \
    --with-openssl=$BUILD_DIR/openssl-${OPENSSL_VERSION} \
    && make &&  make install

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]