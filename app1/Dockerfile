FROM alpine:latest

ENV \
  APP_DIR="/app" \
  APP_PORT="80"

WORKDIR $APP_DIR
COPY . $APP_DIR
COPY .env.example $APP_DIR/.env


# Essentials
RUN echo "UTC" > /etc/timezone
RUN apk add --no-cache zip unzip curl
# Installing bash
RUN apk add bash
RUN sed -i 's/bin\/ash/bin\/bash/g' /etc/passwd

# Installing PHP
RUN apk add --no-cache php8 
    

# Installing composer
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN rm -rf composer-setup.php

RUN composer install
# generate an APP_KEY
RUN php artisan key:generate

CMD php artisan serve --host=0.0.0.0 --port=$APP_PORT
