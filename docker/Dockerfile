FROM php:7.4-fpm-buster

# Install php extensions
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions mysqli pdo_mysql

# Enable "allow_url_fopen" in php.ini
RUN echo "allow_url_fopen = on" >> $PHP_INI_DIR/php.ini

# Install dependencies
RUN apt-get update && apt-get install -y gnupg debian-keyring debian-archive-keyring apt-transport-https && \
    curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/cfg/gpg/gpg.155B6D79CA56EA34.key' | apt-key add - && \
    curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/cfg/setup/config.deb.txt?distro=debian&version=any-version' | tee -a /etc/apt/sources.list.d/caddy-stable.list && \
    apt-get update && apt-get upgrade -y jq unzip gnupg caddy netcat

# Entrypoint and Caddyfile
COPY Caddyfile /etc/caddy/Caddyfile
COPY ember-entrypoint /usr/local/bin/
RUN chmod +x /usr/local/bin/ember-entrypoint
ENTRYPOINT [ "ember-entrypoint" ]
