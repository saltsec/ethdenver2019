FROM ubuntu

RUN apt-get update; apt-get -y upgrade; apt-get install -y build-essential wget libpcre3-dev zlib1g-dev git curl jq
WORKDIR /var/tmp
RUN apt-get install -y openssl libssl-dev
RUN curl -sL $(curl -s https://api.github.com/repos/openresty/openresty/releases/latest |jq -r .assets[].browser_download_url |grep gz) >openresty.tgz
RUN tar zxvf openresty.tgz && cd openresty-* && \
    ./configure \
			--without-http_echo_module \
			--without-http_xss_module \
			--without-http_coolkit_module \
			--without-http_set_misc_module \
			--without-http_encrypted_session_module \
			--without-http_srcache_module \
            --without-http_array_var_module \
            --without-http_memc_module \
            --without-http_redis2_module \
            --without-http_redis_module \
            --without-http_rds_json_module \
            --without-http_rds_csv_module \
            --without-ngx_devel_kit_module \
            --without-http_ssl_module \
            --without-lua_redis_parser \
            --without-lua_rds_parser \
            --without-lua_resty_dns \
            --without-lua_resty_memcached \
            --without-lua_resty_redis \
            --without-lua_resty_mysql \
            --without-lua_resty_upload \
            --without-lua_resty_upstream_healthcheck \
            --without-lua_resty_string \
            --without-lua_resty_websocket \
            --without-lua_resty_lock \
            --without-lua_resty_lrucache \
            --without-select_module \
            --without-poll_module \
            --without-http_gzip_module \
            --without-http_ssi_module \
            --without-http_userid_module \
            --without-http_access_module \
            --without-http_auth_basic_module \
            --without-http_autoindex_module \
            --without-http_geo_module \
            --without-http_map_module \
            --without-http_split_clients_module \
            --without-http_referer_module \
            --without-http_fastcgi_module \
            --without-http_uwsgi_module \
            --without-http_scgi_module \
            --without-http_memcached_module \
            --without-http_empty_gif_module \
            --without-http_browser_module \
            --without-http_upstream_hash_module \
            --without-http_upstream_ip_hash_module \
            --without-http_upstream_least_conn_module \
            --without-http_upstream_keepalive_module \
            --without-http_upstream_zone_module \
            --without-http-cache \
            --without-mail_pop3_module \
            --without-mail_imap_module \
            --without-mail_smtp_module \
            --without-stream_limit_conn_module \
            --without-stream_access_module \
            --without-stream_geo_module \
            --without-stream_map_module \
            --without-stream_split_clients_module \
            --without-stream_return_module \
            --without-stream_upstream_hash_module \
            --without-stream_upstream_least_conn_module \
            --without-stream_upstream_zone_module && \
	make && \
	make install
WORKDIR /usr/local/openresty
RUN rm -fr /var/tmp/openresty*
COPY nginx.conf /usr/local/openresty/nginx/conf/nginx.conf

CMD ["/usr/local/openresty/bin/openresty","-g","daemon off;"]

