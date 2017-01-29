# Docker Hugo Nginx

Docker image to build and deploy [Hugo](http://gohugo.io/) site with nginx. 
Perfect for depolying static sites built with hugo on [dokku](http://dokku.viewdocs.io/dokku/).

Mounts the current directory into a docker `nginx:stable-alpine` image and builds it with `hugo`.

```Dockerfile
FROM martinffx/docker-hugo-nginx

ADD . /usr/src
RUN hugo
```
