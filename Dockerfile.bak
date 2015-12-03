#Dockerfile
FROM daocloud.io/geyijun/basic_image
MAINTAINER geyijun<geyijun@xiongmaitech.com>

COPY resty/ /root/
COPY nginx_http_push_module-master.zip /root/
RUN set -x \
 && cd /root \
 && echo "==> Downloading OpenResty..." \
 && wget http://openresty.org/download/ngx_openresty-1.9.3.1.tar.gz \
 && tar -zxvf ngx_openresty-1.9.3.1.tar.gz	\
 && unzip nginx_http_push_module-master.zip	\
 && cd ngx_openresty-1.9.3.1 	\
 && echo "==> Configuring OpenResty..." \
 && ./configure \
    --with-luajit \
    --with-pcre-jit \
    --without-http_ssl_module \
    --without-http_ssi_module \
    --without-http_userid_module \
    --without-http_uwsgi_module \
    --without-http_scgi_module	\
    --add-module=../nginx_http_push_module-master/	\
 && echo "==> Building OpenResty..." \
 && make \
 && echo "==> Installing OpenResty..." \
 && make install \
 && echo "==> Finishing..." \
 && cd .. && pwd && ls -l \
 && cp -rfp /root/resty/*  /usr/local/openresty/lualib/resty/	\
 && rm -rf /root/ngx_openresty*	\
 && rm -rf /root/nginx_http_push_module-master.zip	\
 && ln -s /usr/local/openresty/nginx/sbin/nginx /usr/bin/nginx
