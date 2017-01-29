# Docker Hugo Nginx

Docker image to build and deploy [Hugo]() site with nginx. Perfect for depolying static sites built with hugo on [dokku]().

Mounts the current directory into a docker `nginx:stable-alpine` image and builds it with `hugo`.

```Dockerfile
FROM nginx:stable-alpine

ENV HUGO_VERSION 0.18.1
ENV SIGIL_VERSION 0.4.0

VOLUME /usr/src
WORKDIR /usr/src
RUN apk add --no-cache --virtual .deps curl tar && \
    curl -L https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz > \
    hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
    tar -zxvf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
    mv hugo_${HUGO_VERSION}_linux_amd64/hugo_${HUGO_VERSION}_linux_amd64 /bin/hugo && \
    rm -rf hugo_${HUGO_VERSION}_linux_amd64 && \
    apk del .deps

COPY ./nginx.conf /etc/nginx/nginx.conf

ONBUILD ADD . /usr/src
ONBUILD RUN hugo
```
