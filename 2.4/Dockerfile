# My httpd image, based on Alpine Linux, configured and forked from the
# official HTTPd Docker repository.
# @see: https://store.docker.com/images/httpd
FROM httpd:2.4-alpine

# Enable some modules.
RUN sed -i 's@^#LoadModule deflate_module modules/mod_deflate.so@LoadModule deflate_module modules/mod_deflate.so@g' /usr/local/apache2/conf/httpd.conf && \
	sed -i 's@^#LoadModule expires_module modules/mod_expires.so@LoadModule expires_module modules/mod_expires.so@g' /usr/local/apache2/conf/httpd.conf && \
	sed -i 's@^#LoadModule http2_module modules/mod_http2.so@LoadModule http2_module modules/mod_http2.so@g' /usr/local/apache2/conf/httpd.conf && \
    sed -i 's@^#LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so@LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so@g' /usr/local/apache2/conf/httpd.conf && \
	sed -i 's@^#LoadModule proxy_http_module modules/mod_proxy_http.so@LoadModule proxy_http_module modules/mod_proxy_http.so@g' /usr/local/apache2/conf/httpd.conf && \
	sed -i 's@^#LoadModule proxy_module modules/mod_proxy.so@LoadModule proxy_module modules/mod_proxy.so@g' /usr/local/apache2/conf/httpd.conf && \
	sed -i 's@^#LoadModule rewrite_module modules/mod_rewrite.so@LoadModule rewrite_module modules/mod_rewrite.so@g' /usr/local/apache2/conf/httpd.conf && \
    sed -i 's@^#LoadModule socache_shmcb_module modules/mod_socache_shmcb.so@LoadModule socache_shmcb_module modules/mod_socache_shmcb.so@g' /usr/local/apache2/conf/httpd.conf && \
	sed -i 's@^#LoadModule ssl_module modules/mod_ssl.so@LoadModule ssl_module modules/mod_ssl.so@g' /usr/local/apache2/conf/httpd.conf

# Add PUID / PGID support
ENV PUID=82
ENV PGID=82
RUN set -eux; \
	apk add --no-cache \
		shadow

# Use port 443
RUN sed -i 's@Listen 80@Listen 80\nListen 443@g' /usr/local/apache2/conf/httpd.conf
EXPOSE 443

# Custom configuration.
RUN mkdir /usr/local/apache2/conf/conf.d && \
    mkdir /usr/local/apache2/conf/vhost.d && \
    mkdir /usr/local/apache2/conf/ssl && \
    echo 'IncludeOptional conf/conf.d/*.conf' >> /usr/local/apache2/conf/httpd.conf
COPY conf.d /usr/local/apache2/conf/conf.d

# Override CMD for PUID / PGID support
COPY --chmod=755 httpd-foreground /usr/local/bin/

WORKDIR /var/www
