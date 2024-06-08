ARG PHP_VERSION=8.3
ARG COMPOSER_VERSION=latest

FROM composer:${COMPOSER_VERSION} AS composer

FROM php:8.3-cli-alpine as base
RUN apk add --no-cache git zip bash
COPY --from=composer /usr/bin/composer /usr/bin/composer

ARG USER_ID=1000
RUN adduser -u ${USER_ID} -D -H app
USER app

COPY --chown=app .. /app
WORKDIR /app

EXPOSE 8337

CMD ["php", "-S", "0.0.0.0:8337", "-t", "public"]