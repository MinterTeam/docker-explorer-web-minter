FROM nginx:alpine

ARG EXPLORER_URL

ENV APP_EXPLORER_URL=$EXPLORER_URL

RUN apk update && \
    apk upgrade && \
    apk --no-cache add build-base automake autoconf nasm nginx nodejs git gifsicle libjpeg-turbo-utils optipng \
                       libtool zlib zlib-dev libpng libpng-dev libwebp libwebp-dev libjpeg-turbo libjpeg-turbo-dev

# Create app directory
WORKDIR /var/www

RUN \
    git clone --single-branch -b dev https://github.com/MinterTeam/minter-explorer-web.git && \
    cd minter-explorer-web && \
    npm install && npm run production

ADD /config/vhost.conf /etc/nginx/conf.d/default.conf

EXPOSE 80