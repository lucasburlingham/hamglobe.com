# lightweight Caddy base with PHP-FPM support
FROM caddy:2-alpine

# install php-fpm and common extensions
RUN apk add --no-cache \
    php8 php8-fpm php8-cli php8-opcache php8-pdo php8-pdo_mysql \
    php8-mbstring php8-json php8-openssl php8-session \
    && mkdir -p /run/php

# set working directory for application
WORKDIR /var/www/html

# copy application code (mount in compose if desired)
COPY . .

# ensure www-data owns files
RUN chown -R www-data:www-data /var/www/html

# default Caddyfile (can be overridden by mounting)
COPY Caddyfile /etc/caddy/Caddyfile

# expose http port
EXPOSE 80

# start php-fpm then caddy; both run in foreground
CMD ["/bin/sh", "-c", "php-fpm8 && caddy run --config /etc/caddy/Caddyfile --watch"]
